# [Build a DIY security camera with neural compute stick - Tutorial](https://www.dlology.com/blog/build-a-diy-security-camera-with-neural-compute-stick-part-2/)
## Introduction
This project uses SSD MobileNet to do object recognition and classification for a webcam.
The companion Arduino sketch can be downloaded from repo [CamGimbal](https://github.com/Tony607/CamGimbal).

The provided Makefile does the following:
1. Builds caffe ssd mobilenet graph file from the caffe/SSD_MobileNet directory in the repository.
2. Copies the built NCS graph file from the SSD_MobileNet directory to the project base directory
3. Downloads some sample traffic video files.
4. Runs the provided video_objects_threaded.py program which creates a GUI window that shows the video stream along with labels and boxes around the identified objects.

## Prerequisites
This program requires:
- 1 NCS device
- NCSDK 2.04 or greater
- OpenCV 3.3 with Video for Linux (V4L) support and associated Python bindings*.

*It may run with older versions but you may see some glitches such as the GUI Window not closing when you click the X in the title bar, and other key binding issues.


Note: The OpenCV version that installs with the current ncsdk (1.10.00) does <strong>not</strong> provide V4L support. Check the [Part 1](https://www.dlology.com/blog/build-a-diy-security-camera-with-neural-compute-stick-part-1/) tutorial to "Install OpenCV3 the easy way"


Note: All development and testing has been done on Ubuntu 16.04 on an x86-64 machine as well as Raspbian Stretch on Raspberry Pi 3 Model B.


This applications is similar to the apps/video_objects application in the ncappzoo, but it adds threads for reading from the video file and processing SSD MobieNet inferences.  This change increases performance on most systems pushing closer to the  max frame rate of the neural network.

## Makefile
Provided Makefile has various targets that help with the above mentioned tasks.

### make help
Shows available targets.

### make run_cam
Runs the provided python program which shows the webcam live video stream along with the object boxes and classifications. Save 'person' images to folder `images`.

### make run_gimbal
Runs the provided python program which shows the webcam live video stream along with the object boxes and classifications. Save 'person' images to folder `images`. Connect to Arduino serial port turning a servo motor to follow one or more detected persons. Check [part 2]((https://www.dlology.com/blog/build-a-diy-security-camera-with-neural-compute-stick-part-2/)) of the tutorial on how to build one yourself.

### make all
Builds and/or gathers all the required files needed to run the application except building and installing opencv (this must be done as a separate step with 'make opencv'.)

### make videos
Downloads example video files.

### make run
Runs the provided python program which shows the video stream along with the object boxes and classifications.

### make clean
Removes all the temporary files that are created by the Makefile
