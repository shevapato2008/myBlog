---
layout: post
title: TensorFlow Environment Setup Under Linux Environment
meta: This post helps set up the TensorFlow environment under Linux environment.
comments: true
mathjax: true
---

**I assume you have already installed the anaconda package on your Linux system.** It does not matter which Anaconda version. Anaconda 2 or 3 would both work.

If you have not installed Anaconda, please download [Anaconda](https://www.continuum.io/downloads) and follow the instructions.

<br>

## Step 1: Create the TensorFlow environment
---
For python 2.7,
```shell
$ conda create -n tensorflow2 python=2 anaconda
```

It's pretty straightforward.
+ **`conda create`** makes the new environment,
+ **`-n tensorflow2`** is the name of the environment,
+ **`python=2`** specifies the python version, i.e. 2.x, and
+ **`anaconda`** says that you want this environment to have access to all packages in the anaconda distribution.

You may create another TensorFlow environment for python 3.x as follows.
```shell
$ conda create -n tensorflow3 python=3 anaconda
```

We will omit the python 3 part below to avoid redundancy.

<br>

## Step 2: Activate the conda environment
---
```shell
$ source activate tensorflow2
(tensorflow2) [..]$ # Your prompt should change.
```
<br>

## Step 3: Install TensorFlow inside your conda environment
---
```shell
(tensorflow) [..]$ pip install --ignore-installed --upgrade tfBinaryURL
```
where `tfBinaryURL` is the [URL of the TensorFlow Python package](https://www.tensorflow.org/install/install_linux#the_url_of_the_tensorflow_python_package "TensorFlow Python packages"). For example, the following command installs the CPU-only version of TensorFlow for Python 2.7:
```shell
(tensorflow) [..]$ pip install --ignore-installed --upgrade \
https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.2.1-cp27-none-linux_x86_64.whl
```

<br>

## Step 4: Validate the TensorFlow Installation
---
Run a short TensorFlow program.
+ Invoke python from your shell as follows:
```shell
$ python
```
+ Enter the following short program inside the python interactive shell:
```shell
# Python
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
```
It should output:
```shell
Hello, TensorFlow!
```

<br>

## Step 5: Use TensorFlow in Jupyter Notebook
---
+ To check if you have already installed Jupyter within the tensorflow environment. Type the following command after activating the tensorflow environment. In our `tensorflow2` case, we type:
```shell
(tensorflow2) [..]$ which jupyter
```
The result:
```shell
(tensorflow2) [..]$ <anaconda_home>/envs/tensorflow/bin/jupyter # installed within the tensorflow environment.
(tensorflow2) [..]$ <anaconda_home>/bin/jupyter                 # not installed.
```
+ If not installed, type the following command.
```shell
(tensorflow2) [..]$ pip install jupyter
```

<br>

## More: About Managing Conda Enironments
---
+ List all environments
```shell
$ conda info --envs
```
Or equivalently,
```shell
$ conda env list
```

+ Remove an environment
```shell
conda remove --name [Environment Name] --all
```

<br><br>

## Reference
---
+ [Installing TensorFlow on Ubuntu](https://www.tensorflow.org/install/install_linux)
+ [The URL of the TensorFlow Python package](https://www.tensorflow.org/install/install_linux#the_url_of_the_tensorflow_python_package)
+ [Managing Conda Environments](https://conda.io/docs/using/envs.html)

**More on Trouble Shooting**<br>
+ [StackOverflow] [Trouble with TensorFlow in Jupyter Notebook](https://stackoverflow.com/questions/37061089/trouble-with-tensorflow-in-jupyter-notebook)
+ [StackOverflow] [HOW TO: Import TensorFlow in Jupyter Notebook from Conda with GPU support?](https://stackoverflow.com/questions/38233996/how-to-import-tensorflow-in-jupyter-notebook-from-conda-with-gpu-support)
+ [StackOverflow] [Can I installed tensorflow for python 2.7 and 3.5 on my machine simultaneously?](https://stackoverflow.com/questions/37863377/can-i-installed-tensorflow-for-python-2-7-and-3-5-on-my-machine-simultaneously)
+ [Reddit] [Installing Anaconda2 & Anaconda3 concurrently](https://www.reddit.com/r/Python/comments/4pqc61/installing_anaconda2_anaconda3_concurrently/)
