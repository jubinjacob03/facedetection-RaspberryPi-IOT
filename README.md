# facedetection-RaspberryPi-IOT
Face detection by Computer Vision using Library file - openCV , on Raspberry Pi  . 

# Requirements 
- Raspberry Pi 3+ (Having the extra computing power 'oomph' that the Pi provides is invaluable)
- Raspberry Pi Official Camera Module V2 (You can also use the Raspberry Pi High-Quality Camera)
- Micro SD Card 
- Power Supply 
- Monitor
- HDMI Cord 
- Mouse and Keyboard

# Installation 
- Download & Flash Raspberry OS on to the Micro SD Card using Raspberry Pi Imager.
- Connect the Raspberry Pi to monitor with peripheries and make sure that the Pi Camera is installed in the correct slot.
- Open up the Raspberry Pi Configuration menu (found using the top left Menu and scrolling over preferences) and enable the Camera found under the Interfaces tab.
- After enabling reset the Raspberry Pi.
- Copy or clone git module files into any directory in the Raspberry OS. Now you can intiate the face detection module.

# Packages to install

<h4>:exclamation: This will be a long stream of terminal commands forewarning. This will also take a substantial amount of time.</h4>

<em>
  
pip install picamera[array]

Sudo apt-get update

Sudo apt-get upgrade

sudo apt install cmake build-essential pkg-config git

sudo apt install libjpeg-dev libtiff-dev libjasper-dev libpng-dev libwebp-dev libopenexr-dev

sudo apt install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libdc1394-22-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

sudo apt install libgtk-3-dev libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5

sudo apt install libatlas-base-dev liblapacke-dev gfortran

sudo apt install libhdf5-dev libhdf5-103

sudo apt install python3-dev python3-pip python3-numpy  </em>

We must now expand the swapfile before running the next set of commands. To do this type and enter into the Terminal the following line.

<em>sudo nano /etc/dphys-swapfile   </em>
 
The change the number on CONF_SWAPSIZE = 100 to CONF_SWAPSIZE=2048. Having done this press Ctrl-X, Y, and then Enter Key to save these changes. This change is only temporary and we will be changing it back. To have these changes affect anything we must restart the swapfile by entering the following command to the terminal. Then we will resume Terminal Commands as normal.

<em>
sudo systemctl restart dphys-swapfile

git clone https://github.com/opencv/opencv.git

git clone https://github.com/opencv/opencv_contrib.git

mkdir ~/opencv/build

cd ~/opencv/build

cmake -D CMAKE_BUILD_TYPE=RELEASE \

-D CMAKE_INSTALL_PREFIX=/usr/local \

-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \

-D ENABLE_NEON=ON \

-D ENABLE_VFPV3=ON \

-D BUILD_TESTS=OFF \

-D INSTALL_PYTHON_EXAMPLES=OFF \

-D OPENCV_ENABLE_NONFREE=ON \

-D CMAKE_SHARED_LINKER_FLAGS=-latomic \

-D BUILD_EXAMPLES=OFF ..

make -j$(nproc)
</em>


This | make | Command will take over an hour to install and there will be no indication of how much longer it will take. It may also freeze the monitor display. Be ultra patient and it will work. Once complete you are most of the way done. Then you can resume terminal commands.

<em>sudo make install

sudo ldconfig

pip install face-recognition --no-cache-dir </em>  



This | pip install face-recognition| Command will take over 40 mins to install and there will be no indication of how much longer it will take. Be ultra patient and it will work. Once complete you are most of the way done. Then we will resume terminal commands.


<em>pip install imutils </em>   


We must now return the swapfile before running the next set of commands. To do this type into Terminal this line.


<em>sudo nano /etc/dphys-swapfile </em>   


The change the number on CONF_SWAPSIZE = 2048 to CONF_SWAPSIZE=100. Having done this press Ctrl-X, Y, and then Enter Key to save these changes. This returns the Swapfile to normal. To have these changes affect anything we must restart the swapfile by entering the following command to the terminal. Then we will resume terminal Commands as normal.


<em>sudo systemctl restart dphys-swapfile  </em>

# Running the Module
- Before loading the module, setup all the required packages mentioned in [Packages section](#packages-to-install)
- Locate the file named 'dataset_picam.py' in root directory, ( eg- home/pi/facedetection-RapsberryPi-IOT/dataset_picam.py ).
- Right Click on the file and open that Python Script up with either Thonny or Geany. Edit the line <code>name = 'Jubin' #replace with your name</code> and change value of name variable to your <em><strong>target person's name</strong></em> and save the file.
- Go back to the parent directory and locate the folder called "dataset" and create a subfolder with the name that you just changed in python script, Because this is where the dataset training image will be saved.
- Jump back to the Python editor (dataset_picam.py) and run the code. This will then open up a little window and a terminal window which you can use to save images of your face. Press <em><strong>Spacebar Key</strong></em> to take a picture (take around 10) and then <em><strong>Q key</strong></em> to close the window.
- Now the images of your face will be stored in the folder you created for your name.
- Open up a new terminal using the black console button on the top left and type the following command and pressing <em><strong>enter</strong></em> after each line. 
  <p><code> cd facedetection-RapsberryPi-IOT  </code></p>
  <p><code>  python train_model.py </code></p> 
- This will start the training process which you can see occurring for each image that you took of your face. After completion the Raspberry Pi will have learned what your face looks like.
- Open a new terminal. Then type the following and press <em><strong>enter</strong></em> after each step.
  <p><code> cd facedetection-RapsberryPi-IOT </code></p>
  <p><code> python facial_recog.py </code></p>
- A small window pop up with a live stream of the Raspberry Pi Camera searching for faces and when it has been supplied with one it will draw a square box around the face. It will also determine if it is a known face displaying Unknown if it is not a known face and the name of the person if it is.
- NOTE : If you tip your head to the side a couple of degrees it will completely disable facial recognition and if you cover your nose it struggles as well. Close the terminal window or press <em><strong>Ctrl C</strong></em> on the Keyboard to stop the script running.

# Help and Reference

<mark><h3>Files inside this project -</h3></mark>
<p><ol>
<li> dataset_picam.py : Python Script used to capture train data images when using Raspberry PI camera module.</li>
<li> dataset_nrmlcam.py : Python Script used to capture train data images using other camera modules.</li>
<li> facial_recog.py : Main python script, running this will intiate Face Recognition Module.</li> 
<li> train_model.py : Python Script for training test data to Computer Vision using machine Learning.</li>
<li> haarcascade_frontalface_default.xml : Xml file that contains face_recognition codecs.</li>
<li> dataset_folder : This is the parent folder of individual target person subfolder where test data images are stored.</li>
<li> photo_folder : This is where output images will be saved.</li>
</ol></p>
<br>

- For learning more about openCV visit [opencv.org](https://docs.opencv.org/4.x/d9/df8/tutorial_root.html).
- Project reference link [here](https://pyimagesearch.com/2018/06/25/raspberry-pi-face-recognition/).
