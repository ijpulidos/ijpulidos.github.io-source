# Compiling Tensorflow from sources in Red Hat Enterprise 7

Among all the things I'm involved with, voluntarily or not, one of them is
administrating a HPC server for some research group at a local university.
Lately I've been asked that they are needing [Tensorflow](www.tensorflow.org),
as you should know it's the famous symbolic math and machine learning software
library from Google.

Sadly there aren't easy official installers for Red Hat Enterprise 7, which is
what the server I admin uses. So, this means I had to compile it from sources, in
this post I'll guide you to the process of installing it.

First I want to point out that I'm using the EPEL extra repositories for my RHE
setup, you may information about setting them [here](https://access.redhat.com/solutions/3358).

## 1. Installing dependencies

Firs is installing the dependencies, basically that means installing some python
libs and the testing/build software Bazel, for the python dependencies you could
just use the yum package manager to install them using the following command
(this is done for `python2`, if you want `python3` just change names accordingly):

    yum install python2-pip python-wheel python-devel numpy

Later we have to install bazel, fortunately there's a fedora/CentOS7 repository
that helps for installing this, you just have to download the `*.repo` file and
save it to your `/etc/yum.repos.d/` directory, detailed information can be found
[here](https://copr.fedorainfracloud.org/coprs/vbatts/bazel/). After that it
would be just running `yum install bazel` command and it all should go smoothly.

### (Optional) GPU support prerequisites

If you need to install Tensorflow with GPU capabilities (basically it is CUDA
capabilities) you will also need to install the CUDA SDK, cuDNN SDK and CUPTI.
Take into account that you need CUDA Compute Capability 3.0 or higher for this
to work.

#### CUDA

I won't go into much detail on how to install CUDA, but basically I just
followed the official nvidia documentation which you can find [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#redhat-installation)

#### cuDNN

As with CUDA, I just followed the official installation instruction in
https://docs.nvidia.com/deeplearning/sdk/cudnn-install/ , you just have to
consider the CUDA version you have installed on your system and download the
cuDNN version accordingly. Also, you can get the code samples from the .deb
installer just opening it with any archive manager tool that can handle tar
archives and xz compression, you find the samples in the `usr/src/` path inside
the `data.tar.xz` which is, in turn, inside the `.deb` file.

#### CUPTI

As the [Tensorflow install instructions] say, you just have to add the CUPTI
path to your `LD_LIBRARY_PATH`, for example by adding to your `~/.bashrc` file
the following line:

    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64 

## 2. Cloning and building TensorFlow

We will be installing TensorFlow from the very [git sources at github](https://github.com/tensorflow/tensorflow).
For this we will need to have `git` installed on our system and clone the
repository using the following command:

    git clone https://github.com/tensorflow/tensorflow

this will create a directory named `tensorflow` in whatever directory we run
this command from, that is, our current working directory.

### Configuring installation

Once you have cloned the `tensorflow` sources you should run the configuration
script by running the `./configure` command inside the root directory of
tensorflow. This will ask you many questions about your desired setup, for
example if you will use AWS or Google Cloud or CUDA and a lot of other options
available. In my case I just set it up to use CUDA and had to tell the script to
find CUDA in the correct path with the correct versions. This step depends a lot
on your specific configuration so you should just read about the different
options in the official [install instructions](https://www.tensorflow.org/install/install_sources#ConfigureInstallation).


