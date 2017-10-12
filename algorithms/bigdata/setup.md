---
layout: algorithm
comments: true
mathjax: true
---

# Setup Hadoop Ecosystem Using Docker for Ubuntu 16.04

<br>

Docker is a ground breaking improvement nowadays which provides a convenient way to setup big data environment. This article will briefly go over the basic steps in building up your own hadoop environment using Docker CE (community edition).

<br>

## Docker Installation
---
First of all, you need to follow the official instructions from Docker to get docker installed.<br>
[Get Docker CE for Ubuntu](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce "https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce")

You may also find the follow link useful if you are in China. The Aliyun mirror provides a faster source to get installation files.<br>
[阿里云Docker CE镜像源站](https://yq.aliyun.com/articles/110806?spm=5176.100239.blogcont29941.16.RM1yMV "https://yq.aliyun.com/articles/110806?spm=5176.100239.blogcont29941.16.RM1yMV")

Run the following commands to check if docker is properly installed.
```shell
$ sudo docker info
```

<br>

## Setup Hadoop Ecosystem
---
Build a working directory and enter it.
```shell
$ mkdir bigData
$ cd bigData
```
Pull docker image.
```shell
$ sudo docker pull kiwenlau/hadoop:1.0
```
Clone github repository.
```shell
$ git clone https://github.com/kiwenlau/hadoop-cluster-docker
```
Create hadoop network.
```shell
$ sudo docker network create --driver=bridge hadoop
```
Start docker container.
```shell
$ cd hadoop-cluster-docker
$ sudo ./start-container.sh
```
Output:
>```
start hadoop-master container...
start hadoop-slave1 container...
start hadoop-slave2 container...
root@hadoop-master:~#
```

+ Started 3 containers with 1 master and 2 slaves.
+ You will get into the `/root` directory of `hadoop-master` container.

Start hadoop.
```shell
root@hadoop-master:~# ./start-hadoop.sh
```
Run wordcount.
```shell
root@hadoop-master:~# ./run-wordcount.sh
```
Output:
>```
>input file1.txt:
>Hello Hadoop
>
>input file2.txt:
>Hello Docker
>
>wordcount output:
>Docker	1
>Hadoop	1
>Hello	2
>```

If something like above appears as an output, that means you have successfully deployed hadoop ecosystem using docker.

<br>

## Further Test Hadoop Ecosystem in Docker
---
Use WordCount as an example. Run the following code in docker.

Copy and paste the following code in terminal.
```shell
echo "
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

public class WordCount {

    public static class TokenizerMapper extends
            Mapper<Object, Text, Text, IntWritable> {

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context)
                throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
                word.set(itr.nextToken());
                context.write(word, one);
            }
        }
    }

    public static class IntSumReducer extends
            Reducer<Text, IntWritable, Text, IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                Context context) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
                sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = new Job(conf, \"word count\");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
" > WordCount.java
```

```
root@hadoop-master:~# ls
WordCount.java  hdfs  run-wordcount.sh  start-hadoop.sh
```



<br><br>
