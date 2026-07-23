# My Project
#   Country Flag Recognition

This project uses a trained artificial intelligence model to detect and classify Country Flags.

The model was trained using the ImageNet architecture with NVIDIA's Jetson-inference library and is optimized to run efficiently on a Jetson Orin Nano.


# hardware for the Project:

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

here are the following steps for the project:
 
 first you have to download the Dataset. 
<pre><code>#!/bin/bash
curl -L -o ~/Downloads/world-flags-dataset-195.zip\
  https://www.kaggle.com/api/v1/datasets/download/shuvokumarbasak4004/world-flags-dataset-195</code></pre>

Next you have to change directory.
<pre><code>
cd jetson-inference/python/training/classification/data</code></pre>

You may need to create a subfolder to store the files in depending on if the dataset comes with one or not which in this case it will be required.


<pre><code>
now you have to unzip the files from your downloads. The -d flag CAN be omitted IF you didn't create a subfolder:
unzip ~/Downloads/your_dataset.zip -d subfolder_name</code></pre>

And now you will organize the Dataset (test/val/train)
<pre><code>
python3 reshape.py</code></pre>



In your dataset directory create a new file named labels.txt. In labels.txt, put each country in alphabetical order. It won't work unless it is all in alphabetical order.


after you have put it all in alphabetical order run the docker container: 



<pre><code>
cd ~/jetson-inference/
./docker/run.sh</code></pre>

Navigate into your classification folder with this command:

<pre><code>
cd python/training/classification</code></pre>

<pre><code>
python3 train.py --model-dir=models/Your_Model data/dataset</code></pre>

and IF you want to change the training amount change the epoch= with a smaller number for shorter training and a bigger number for longer training
<pre><code>
python3 train.py --epochs=10 --model-dir=models/Your_Model data/dataset</code></pre>

now run the ONNX export script:
<pre><code>
python3 onnx_export.py --model-dir=models/Your_Model</code></pre>

exit the docker container with
<pre><code>
Ctrl + d</code></pre>

Set the variables
<pre><code>
NET=models/Your_Model
DATASET=data/dataset</code></pre>

And finally run the AI for your newly completed project with
<pre><code>
imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/dataset/your_image_input output.jpg</code></pre>

With this you'll have a new fully functioning country recognition AI!
