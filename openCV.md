
# OpenCV  
### *Last Updated: 31-01-2021 Ubuntu 18*
### **Manuel Rios & Jorge Mora**

## OpenCV 4

Run the following lines on terminal to insall openCV dependencies:  


```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential cmake unzip pkg-config
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk-3-dev
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python3-dev
```

Download OpenCV

Let's download `opencv` and `opencv_contrib` on our home directory

```
cd ~
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.0.0.zip
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.0.0.zip
```

Then unzip the file and rename it

```
unzip opencv.zip
unzip opencv_contrib.zip
mv opencv-4.0.0 opencv
mv opencv_contrib-4.0.0 opencv_contrib
rm opencv.zip
rm opencv_contrib.zip
```

In order to compile OpenCV from source, we will need a Python3 virtual environment with numpy installed. Once you got that, activate the environment.  
Then run the following  instructions:

```
cd ~/opencv
mkdir build
cd build
```

Then compile OpenCV, remember to fix the python executable path and check the contrib modules path.  

If you want cuda support run:   

```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D BUILD_opencv_cudacodec=OFF \
    -D WITH_CUDA=ON \
    -D WITH_CUDNN=ON \
    -D ENABLE_FAST_MATH=1 \
    -D CUDA_FAST_MATH=1 \
    -D WITH_CUBLAS=1 \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D PYTHON_EXECUTABLE=/home/manuel/PythonEnvs/opencv4_env/bin/python \
    -D BUILD_EXAMPLES=ON ..
```

else, run: 


```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D INSTALL_C_EXAMPLES=OFF \
	-D OPENCV_ENABLE_NONFREE=ON \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
	-D PYTHON_EXECUTABLE=~/.virtualenvs/cv/bin/python \
	-D BUILD_EXAMPLES=ON ..
```

finalluy, compile and install openCV

```
make -j4
sudo make install
sudo ldconfig
```

Now lets rename OpenCV bindings, The SO file name and python versions may vary in your computer.

```
cd /usr/local/python/cv2/python-3.6
sudo mv cv2.cpython-36m-x86_64-linux-gnu.so cv2.so
```

Finally create a sym-link to you python env.

```
cd YOUR_ENV/lib/python3.5/site-packages/
ln -s /usr/local/python/cv2/python-3.6/cv2.so cv2.so
```

At this point cv2 should be working on your virtualenv

```
python
import cv2
cv2.__version__
```
