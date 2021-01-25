
# CUDA SETUP  
### *Last Updated: 19-01-2021 Ubuntu 18*
### **Manuel Rios & Jorge Mora**

## CUDA DRIVERS

On terminal run:


```
sudo apt-get purge nvidia *
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
```

Open `Software and Updates` and go to the `Additional drivers`  tab.  
Select The last Nvidia Driver version with the _propietary_ tag at the end of its name.  
Click on Apply Changes.  
Restart the computer.  

## CUDA TOOLKIT

Visit [Nvidia developer](https://developer.nvidia.com/cuda-10.0-download-archive) and select:

- **Operating System** Linux
- **Architecture**: x86_64
- **Distribution**: Ubuntu
- **Version**: 18.04
- **Installer Type**: deb(local)  

Then download the base installer and patch 1.

Open a terminal on the file location and execute:  

```
sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```

Double click the patch 1 to install it.

On terminal run:

`sudo nano ~/.bashrc`

Add the following lines at the end of your .bashrc file 

```
export PATH=/usr/local/cuda-10.0/bin${PATH:+:$PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

Close all terminals.


## cuDNN INSTALLATION

*Note: You need to have an Nvidia Developer Account for this step*


Visit [cuDNN developer](https://developer.nvidia.com/rdp/cudnn-archive):

Click on **cuDNN v7.6.5 (November 5th, 2019), for CUDA 10.0**

Download **cuDNN Library for Linux**

Move the tar file to a desire location and run

```
tar -xzvf cudnn-10.0-linux-x64-v7.6.5.32.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

## Verify it is working

Let's create a python virtual environment and install tensorflow to check if cuda is working properly 

```
python3 -m venv your_env_name
source your_env_name/bin/activate
pip install tensorflow-gpu
```

Start pyhon 

`python`

Run

```
import tensorflow as tf
hello = tf.constant('hello tensorflow')
with tf.Session() as sesh:
    sesh.run(hello)
```

If the tensorflow installation fails try running:

`sudo apt-get install python3-dev`