---
layout: post
title: TensorFlow GPU Setup Under Linux Environment
meta: This post helps set up the TensorFlow GPU version under Ubuntu 16.04 environment.
comments: true
mathjax: true
---

This article gives the detailed instruction for tensorflow gpu installation. In order to use TensorFlow with GPU support you must have a Nvidia graphic card with a minimum compute capability of 3.0. After several unsuccessfull attemps, I finally managed to find the right combination for my `GTX 1060 6gb`: `Ubuntu 16.04` + `CUDA 8.0` + `cuDNN v6` + `Tensorflow 1.3`. Lets get started with the installation.

## Step 1: Update/Install NVIDIA drivers
---
Install up-to-date [NVIDIA drivers](http://www.nvidia.com/Download/index.aspx?lang=en-us) for your GPU.
```shell
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
$ sudo apt-get install nvidia-384 nvidia-settings
```
Reboot to let graphics driver take effect.
Go to `Software & Updates` to verify the version of NVIDIA graphics driver.

<br>

## Step 2: Intall and test CUDA v8.0
---
The NVIDIA® CUDA® Toolkit provides a development environment for creating high performance GPU-accelerated applications. To use TensorFlow with NVIDIA GPUs, the first step is to install the CUDA Toolkit by following the official documentation. You may download it from its official website: [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)

Select `Linux`, `x86_64`, `Ubuntu`, `16.04`, `deb (local)`. Then type the following commands in your Linux terminal.
```shell
$ sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
$ sudo apt-get update
$ sudo apt-get install cuda
```
After installation, you can set the environment variables for CUDA Toolkit by attaching the following PATHs to the end your `~/.bashrc` file.
```shell
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
`${PATH:+:${PATH}}` and `${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}` are just a trick to avoid the possibility of adding an extra colon `:`.
Type the following command to let the change take effect.
```shell
$ source ~/.bashrc
```

Test your CUDA installation.
```shell
$ cd /usr/local/cuda-8.0/samples/5_Simulations/nbody
$ sudo make
$ ./nbody
```
If successful, a new window will popup running n-body simulation.

<br>

## Step 3: Install cuDNN v6
---
The NVIDIA CUDA® Deep Neural Network library (cuDNN) is a GPU-accelerated library of primitives for deep neural networks.

Once the CUDA Toolkit is installed, download cuDNN v6 Library (cuDNN v6 is recommended for TF v1.3) for Linux and install by following the official documentation. (Note: You will need to register for the [Accelerated Computing Developer Program](https://developer.nvidia.com/developer-program)).

Once downloaded, navigate to the directory containing cuDNN:
```shell
$ tar -xzvf cudnn-8.0-linux-x64-v6.0.tgz
$ sudo cp cuda/include/cudnn.h /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
Now that the prerequisites are installed, we can build and install TensorFlow.

<br>

## Step 4: Prepare TensorFlow dependencies and required packages.
---
```shell
$ sudo apt-get install libcupti-dev
```

<br>

## Step 5: Install TensorFlow v1.3 (GPU-accelerated version)
---
There are several ways to install TensorFlow.
+ from sources
+ pip install
+ docker
+ Anaconda

I personally prefer installing based on anaconda. Because it is pretty flexible: the tensorflow environments created using `conda` commands do not interfere with your local python environment. You can check the official sources ([TensorFlow Linux Installation](https://www.tensorflow.org/install/install_linux), [TensorFlow Chinese Community](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html)) for the other installation options.

### Installation based on Anaconda

**0. Prerequisites**<br>
I assume you have already installed the anaconda package on your Linux system. It does not matter which Anaconda version. Anaconda 2 or 3 would both work.

If you have not installed Anaconda, please download [Anaconda](https://www.continuum.io/downloads) and follow the instructions.

**1. Create the TensorFlow environment**<br>
For python 2.7, you can generate a TensorFlow environment using `conda` command as follows.
```shell
$ conda create -n tensorflow1.3-gpu-py2.7 python=2 anaconda
```

It's pretty straightforward.
+ **`conda create`** makes the new environment,
+ **`-n tensorflow1.3-gpu-py2.7`** is the name of the environment,
+ **`python=2`** specifies the python version, i.e. 2.x, and
+ **`anaconda`** says that you want this environment to have access to all packages in the anaconda distribution.

You may create another TensorFlow environment for python 3.x as follows.
```shell
$ conda create -n tensorflow1.3-gpu-py3.6 python=3 anaconda
```

We will omit the python 3 part below to avoid redundancy.

**2. Activate the conda environment**
```shell
$ source activate tensorflow1.3-gpu-py2.7
(tensorflow1.3-gpu-py2.7) [..]$ # Your prompt should change.
```
You can exit your current conda environment by the following command.
```shell
(tensorflow1.3-gpu-py2.7) [..]$ source deactivate
```

**3. Install TensorFlow inside your conda environment**
```shell
(tensorflow) [..]$ pip install --ignore-installed --upgrade tfBinaryURL
```
where `tfBinaryURL` is the [URL of the TensorFlow Python package](https://www.tensorflow.org/install/install_linux#the_url_of_the_tensorflow_python_package "TensorFlow Python packages").

For example, the following two commands install the CPU-only version of TensorFlow or GPU-supported version for Python 2.7 respectively.

```shell
# CPU only version
(tensorflow1.3-gpu-py2.7) [..]$ pip install --ignore-installed --upgrade \
https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.3.0-cp27-none-linux_x86_64.whl

# GPU supported version
(tensorflow1.3-gpu-py2.7) [..]$ pip install --ignore-installed --upgrade \
https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.3.0-cp27-none-linux_x86_64.whl
```

**4. Validate the TensorFlow Installation**<br>
Run a short TensorFlow program.
+ Invoke python from your shell as follows:
```shell
(tensorflow1.3-gpu-py2.7) [..]$ python
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

## Step 6: Use TensorFlow in Jupyter Notebook
---
Check if you have already installed Jupyter within the tensorflow environment. Type the following command after activating the tensorflow environment.
```shell
(tensorflow1.3-gpu-py2.7) [..]$ which jupyter
```
The result `<anaconda_home>/envs/<conda env name>/bin/jupyter` means that jupyter package is installed within the tensorflow environment. The output `<anaconda_home>/bin/jupyter` means that jupyter package is not installed in the tensorflow conda environment.

If not installed, type the following command.
```shell
(tensorflow1.3-gpu-py2.7) [..]$ pip install jupyter
```

<br>

## More: About Managing Conda Environments
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
+ [NVIDIA Official] [GPU-accelerated TensorFlow: Get started today with this GPU-Ready Apps guide.](https://www.nvidia.com/en-us/data-center/gpu-accelerated-applications/tensorflow/)
+ [TensorFlow Official] [Installing TensorFlow on Ubuntu](https://www.tensorflow.org/install/install_linux)
+ [TensorFlow中文社区] [TensorFlow下载与安装](http://www.tensorfly.cn/tfdoc/get_started/os_setup.html)
+ [YouTube] [Installing the GPU version of TensorFlow for making use of your CUDA GPU](https://www.youtube.com/watch?v=io6Ajf5XkaM)
+ [TensorFlow Official] [The URL of the TensorFlow Python package](https://www.tensorflow.org/install/install_linux#the_url_of_the_tensorflow_python_package)
+ [conda.io] [Managing Conda Environments](https://conda.io/docs/using/envs.html)

**More on Trouble Shooting**<br>
+ [StackOverflow] [Trouble with TensorFlow in Jupyter Notebook](https://stackoverflow.com/questions/37061089/trouble-with-tensorflow-in-jupyter-notebook)
+ [StackOverflow] [HOW TO: Import TensorFlow in Jupyter Notebook from Conda with GPU support?](https://stackoverflow.com/questions/38233996/how-to-import-tensorflow-in-jupyter-notebook-from-conda-with-gpu-support)
+ [StackOverflow] [Can I installed tensorflow for python 2.7 and 3.5 on my machine simultaneously?](https://stackoverflow.com/questions/37863377/can-i-installed-tensorflow-for-python-2-7-and-3-5-on-my-machine-simultaneously)
+ [Reddit] [Installing Anaconda2 & Anaconda3 concurrently](https://www.reddit.com/r/Python/comments/4pqc61/installing_anaconda2_anaconda3_concurrently/)
