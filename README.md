# My Project
#   Country Flag Recognition

This project uses a trained artificial intelligence model to detect and classify Country Flags.

The model was trained using the ImageNet architecture with NVIDIA's Jetson-inference library and is optimized to run efficiently on a Jetson Orin Nano.


hardware for the Project:

*   NVIDIA Jetson Orin Nano
*   Jetson-inference 
*   USB Webcam which is optional for real-time inference

# Dataset

The datasets sourced from Kaggle is used for training for the project. It has been restructured to be compatible with the classification requirements of `jetson-inference`. 

this is the dataset i used for my project: https://www.kaggle.com/datasets/shuvokumarbasak4004/world-flags-dataset-195 

The dataset is split using the file systems below:

dataset/

├── train/       # Training images

├── val/         # Validation images

└── test/        # Testing images

## Algorithm

## Running this project

Download the Dataset 
<pre><code>#!/bin/bash
curl -L -o ~/Downloads/cardetection.zip \
  https://www.kaggle.com/api/v1/datasets/download/pkdarabi/cardetection</code></pre>

Change directory
<pre><code>
cd jetson-inference/python/training/classification/data</code></pre>

You may need to create a subfolder to store the files in. This depends on if the dataset comes with one or not. In this case, it's required.


<pre><code>
Unzip the file from your downloads. The -d flag can be omitted if you didn't create a subfolder:
unzip ~/Downloads/your_dataset.zip -d subfolder_name</code></pre>

Now you will organize the Dataset (test/val/train)
<pre><code>
python3 reorganize.py</code></pre>

If you want the exact same project you will may be have to clean or divide the Dataset in only 2 classes


In your dataset directory create a new file. Name it labels.txt. In labels.txt, put each class of objects. Ensure that all of these are in alphabetical order. 


then run the docker container: 


Ensure that all of these are in alphabetical order.

<pre><code>
cd ~/jetson-inference/
./docker/run.sh</code></pre>

Navigate into your classification folder:

<pre><code>
cd python/training/classification</code></pre>

<pre><code>
python3 train.py --model-dir=models/Your_Model data/dataset</code></pre>

and if you want to make the training shorter or longer change the 
<pre><code>epoch</code></pre>

<pre><code>
python3 train.py --epochs=10 --model-dir=models/Your_Model data/dataset</code></pre>

Run the ONNX export script:
<pre><code>
python3 onnx_export.py --model-dir=models/Your_Model</code></pre>

exit the docker container:
<pre><code>
Ctrl + d</code></pre>

Set the variables
<pre><code>
NET=models/Your_Model
DATASET=data/dataset</code></pre>

Run the AI
<pre><code>
imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/dataset/your_image_input output.jpg</code></pre>
