---
layout: algorithm
comments: true
mathjax: true
---

# Word Count

<br>

## Code and Analysis
---
```java
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class wordCount {

	public static class TokenizerMapper extends
			Mapper<Object, Text, Text, IntWritable> {

		// create 2 objects as output of mapper class
		private final static IntWritable one = new IntWritable(1);
		private Text word = new Text();

		@Override
		public void map(Object key, Text value, Context context)
				throws IOException, InterruptedException {
			StringTokenizer itr = new StringTokenizer(value.toString());
			while (itr.hasMoreTokens()) {
				word.set(itr.nextToken());
				context.write(word, one);
			}
		}
	}
	/** Note:
	 * (1) About the 4 Mapper class arguments
	 *    - Object, Text: Mapper input key-value pair
	 *    - Text, IntWritable: Mapper output key-value pair
	 *
	 * (2) About the 3 inputs of the method map()
	 *    - Object key: location in the file
	 *    - Text value: a line of text in the file if '\n' is used as delimiter
	 *    - Context context: Mapper cannot hold the result in
	 *      the memory. Mapper wants to put the result on HDFS. Context helps
	 *      MapReduce to interact with other parts of the system, e.g.
	 *      transferring data.
	 *
	 * (3) Expected output format:
	 *     <word1, 1>, <word1, 1>, <word2, 1>, <word3, 1> ...
	 */


	public static class IntSumReducer extends
			Reducer<Text, IntWritable, Text, IntWritable> {

		// create one object as the final output for mapreduce
		private IntWritable result = new IntWritable();

		@Override
		public void reduce(Text key, Iterable<IntWritable> values,
				Context context)
				throws IOException, InterruptedException {
			int sum = 0;
			for (IntWritable val : values) {
				sum += val.get();
			}
			result.set(sum);
			context.write(key, result);
		}
	}
	/** Note:
	 * (1) output of mapper => shuffle => input of reducer
	 * (2) sample input of reducer:
	 *     <word1, <1, 1>>, <word2, 1>, <word3, 1>, ...
	 * (3) sample output of reducer: <word1, 2>, <word2, 1>, <word3, 1>, ...
	 */

	public static void main(String[] args) throws Exception {
		Configuration conf = new Configuration();
		Job job = new Job(conf, "word count");
		job.setJarByClass(wordCount.class);
		job.setMapperClass(TokenizerMapper.class);
		job.setCombinerClass(IntSumReducer.class);
		job.setReducerClass(IntSumReducer.class);
		job.setOutputKeyClass(Text.class);
		job.setOutputValueClass(IntWritable.class);
		FileInputFormat.addInputPath(job, new Path(args[0]));
		FileOutputFormat.setOutputPath(job, new Path(args[1]));
		System.exit(job.waitForCompletion(true) ? 0 : 1);
	}
	/** Note:
	 * (1) Configuration: sets how you want to separate the input text.
	 *         You may separate it using the default delimiter "\n" or opt
	 *         to use period "." as a delimiter.
	 * (2) Job: tells hadoop which is mapper which is reducer and so on.
	 *         .setJarByClass(): tells hadoop which is the main class
	 *         .setMapperClass(): tells which is the mapper class
	 *         .setReducerClass(): tells which is the reducer class
	 *         .setOutputKeyClass(): tells which is MapReduce output key
	 *         .setOutputValueClass(): tells which is MapReduce output value
	 */
}
```

<br>

## Run the code on HDFS
---
First, start the hadoop-docker containers.
```shell
$ sudo docker pull joway/hadoop-cluster
$ git clone https://github.com/joway/hadoop-cluster-docker
$ sudo docker network create --driver=bridge hadoop
$ cd hadoop-cluster-docker
$ sudo ./start-container.sh 5
```

Copy `wordCount.java` file and [HistoryofPainting.txt]({{site.baseurl}}/algorithms/bigdata/assets/files/HistoryofPainting.txt "Download") to `~/src` shared folder. Then it will appear in the docker container automatically.

```shell
# start container
$ sudo ./start-container.sh

# conpile wordCount.java and make .jar file
root@hadoop-master:~# cd src
root@hadoop-master:~# hadoop com.sun.tools.javac.Main wordCount.java
root@hadoop-master:~# jar cf wc.jar wordCount*.class

# upload the local text file to HDFS
root@hadoop-master:~# hdfs dfs -mkdir -p input
root@hadoop-master:~# hdfs dfs -copyFromLocal /root/src/HistoryofPainting.txt input

# run the mapreduce code on HDFS
root@hadoop-master:~# hdfs dfs -rm -r output
root@hadoop-master:~# hadoop jar wc.jar wordCount input
root@hadoop-master:~# hdfs dfs -cat output/part-r-00000
```

The output should look like the following.
![result]({{site.baseurl}}/algorithms/bigdata/assets/images/wc_java/result.png)

<br><br>
