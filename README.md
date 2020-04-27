# Forklift detection: Internship October 2019 / April 2020

This repo contains the web app that was developed for the forklift detection project based on [YOLOv3](https://pjreddie.com/darknet/yolo/) computer vision algorithm. It includes two different tasks:  
    - Video processing using a model we trained ourselves to detect forklifts
    - Streaming processing to detect cars and people using YOLO
    
## Repo structure
+ [`templates`](/templates/): HTML document
+ [`static`](/static/): Images, javascript and CSS sheet
+ [`model`](/model/): YOLO Scripts and Model weights
+ [`app.py`]: Flask application
+ [`ffmpeg.exe`]: Solution to convert video formats

## Getting Started

### Requisites

YOLO model was employed following this [blog](https://blog.insightdatascience.com/how-to-train-your-own-yolov3-detector-from-scratch-224d10e55de2). 

For the project python was used installing the suggested requirements as indicated in the instructions.

To speed up detections, we counted on **GPU NVIDIA Tesla P40** support. For video processing it may not be needed but for streaming processing it is necessary, otherwise it would not work. 


### Description

#### 1 Video processing

Based on Tiny-yolo model trained with 400 forklift images obtained from google images. 

It permits performing subsumpling indicating the number of frames processed per second

While the video is processed a [progressbar](https://progressbarjs.readthedocs.io/en/latest/) is shown

#### 1b Setting up Virtual Environment [Windows]
Use the [Github Desktop GUI](https://desktop.github.com/) to clone this repo to your local machine. Navigate to the `TrainYourOwnYOLO` project folder and open a power shell window by pressing **Shift + Right Click** and selecting `Open PowerShell window here` in the drop-down menu.

Create Virtual **(Windows)** Environment (requires [venv](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) which is included in the standard library of Python 3.3 or newer):

```
py -m venv env
.\env\Scripts\activate
```
![PowerShell](/Utils/Screenshots/PowerShell.png)
Make sure that, from now on, you **run all commands from within your virtual environment**.

#### 2 Install Required Packages [Windows, Mac or Linux]
Install all required packages with:

```
pip install -r requirements.txt
```
If this fails, you may have to upgrade your pip version first with `pip install pip --upgrade`. If your system has working CUDA drivers, it will use your GPU automatically for training and inference.

## Quick Start (Inference only)
To test the cat face detector on test images located in [`TrainYourOwnYOLO/Data/Source_Images/Test_Images`](/Data/Source_Images/Test_Images) run the `Minimal_Example.py` script in the root folder with:

```
python Minimal_Example.py
```

The outputs are saved in [`TrainYourOwnYOLO/Data/Source_Images/Test_Image_Detection_Results`](/Data/Source_Images/Test_Image_Detection_Results). This includes:
 - Cat pictures with bounding boxes around faces with confidence scores and
 - [`Detection_Results.csv`](/Data/Source_Images/Test_Image_Detection_Results/Detection_Results.csv) file with file names and locations of bounding boxes.

 If you want to detect cat faces in your own pictures, replace the cat images in [`Data/Source_Images/Test_Images`](/Data/Source_Images/Test_Images) with your own images.

## Full Start (Training and Inference)

To train your own custom YOLO object detector please follow the instructions detailed in the three numbered subfolders of this repo:
- [`1_Image_Annotation`](/1_Image_Annotation/),
- [`2_Training`](/2_Training/) and
- [`3_Inference`](/3_Inference/).
 
**To make everything run smoothly it is highly recommended to keep the original folder structure of this repo!**

Each `*.py` script has various command line options that help tweak performance and change things such as input and output directories. All scripts are initialized with good default values that help accomplish all tasks as long as the original folder structure is preserved. To learn more about available command line options of a python script `<script_name.py>` run:

```
python <script_name.py> -h
```

## License

Unless explicitly stated otherwise at the top of a file, all code is licensed under the MIT license. This repo makes use of [**ilmonteux/logohunter**](https://github.com/ilmonteux/logohunter) which itself is inspired by [**qqwweee/keras-yolo3**](https://github.com/qqwweee/keras-yolo3).

## Acknowledgements
Many thanks to [Niklas Wilson](https://github.com/NiklasWilson) for contributing towards making this repo compatible with Tensorflow 2.0. 

## Troubleshooting

0. If you encounter any error, please make sure you follow the instructions **exactly** (word by word). Once you are familiar with the code, you're welcome to modify it as needed but in order to minimize error, I encourage you to not deviate from the instructions above. If you would like to file an issue, please use the provided template and make sure to fill out all fields. 

1. If you encounter a `FileNotFoundError` or a `Module not found` error, make sure that you did not change the folder structure. In particular, your  working directory needs to look like this: 
    ```
    TrainYourOwnYOLO
    └─── 1_Image_Annotation
    └─── 2_Training
    └─── 3_Inference
    └─── Data
    └─── Utils
    ```
    If you want to use a different folder layout (not recommended) you will have to specify your paths as command line arguments. Also, try to avoid spaces in folder names, i.e. don't use a folder name like this `my folder` but instead use `my_folder`.

2. If you are using [pipenv](https://github.com/pypa/pipenv) and are having trouble running `python3 -m venv env`, try:
    ```
    pipenv shell
    ```

3. If you are having trouble getting cv2 to run, try:

    ```
    apt-get update
    apt-get install -y libsm6 libxext6 libxrender-dev
    pip install opencv-python
    ```

4. If you are a Linux user and having trouble installing `*.snap` package files try:
    ```
    snap install --dangerous vott-2.1.0-linux.snap
    ```
    See [Snap Tutorial](https://tutorials.ubuntu.com/tutorial/advanced-snap-usage#2) for more information.

## Filing an Issue
If you would like to file an issue, please use the provided issue template and make sure to complete all fields. This makes it easier to reproduce the issue for someone trying to help you. 

![Issue](/Utils/Screenshots/Issue.gif)

Issues without a completed issue template will be deleted after 7 days. 

## Stay Up-to-Date

- ⭐ **star** this repo to get notifications on future improvements and
- 🍴 **fork** this repo if you like to use it as part of your own project.

![CatVideo](/Utils/Screenshots/CatVideo.gif)
