# Forklift detection: Internship October 2019 / April 2020

This repo contains the web app that was developed for the forklift detection project based on [YOLOv3](https://pjreddie.com/darknet/yolo/) computer vision algorithm. It includes two different tasks:  

    - Video processing using a model we trained ourselves to detect forklifts
    - Streaming processing to detect cars and people using YOLO
    
## Repo structure
+ [templates]: HTML document
+ [static]: Images, javascript and CSS sheet
+ [model]: YOLO Scripts and Model weights
+ [app.py]: Flask application
+ [ffmpeg.exe]: Solution to convert video formats

## Getting Started

### Requisites

YOLO model was employed following this [blog](https://blog.insightdatascience.com/how-to-train-your-own-yolov3-detector-from-scratch-224d10e55de2) and this [repo](https://github.com/AntonMu/TrainYourOwnYOLO). 

For the project python was used installing the suggested requirements as indicated in the instructions.

To speed up detections, we counted on **GPU NVIDIA Tesla P40** support. For video processing GPU may not be needed but for streaming processing it is necessary, otherwise it would not work properly. 

### Description

#### 1 Video processing

Based on Tiny-yolo model trained with 400 forklift images obtained from google images. 

Detects forklifts on mp4 videos. It permits performing subsumpling indicating the number of frames processed per second

While the video is processed a progressbar is shown using this [framework](https://progressbarjs.readthedocs.io/en/latest/)

#### 2 Streaming processing

Based on original YOLO model. 

The initial idea would be to process streaming of forklifts and people working in a ware house. Since that was not possible, it was decided to explore the possibility of accesing streaming cameras focusing on the streets, where cars and people are constantly passing by.

The cameras we worked with are from [skylinewebcams](https://www.skylinewebcams.com), an italian company that installs webcams all around the world to promote tourism. 

The website does not offer an API. But studying its behaviour the links to get the M3U8 files were found, and since these files are clear, we had all that was needed to be able to work with the platform cameras.

<img src="/flow_diagram.png" width="600">

In the diagram, it can be seen the idea of how videos are accesed. It is important to take in count that the length of them all is always 8 seconds, which is the time available to retrieve one, process it with YOLO and load it to the buffer of the web app. This is why a GPU is required. Also subsampling and downsizing was performed in order to append the videos to the buffer as quick as possible.

Nonetheless 

## Acknowledgements
Many thanks to our tutors Emilio Martin Gallardo and Hind Azegrouz that guided us during the project

## Authors
Alejandro Torrado
Javier Esteban Quiles
