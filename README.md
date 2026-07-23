# My Project
#   Country Flag Recognition

This project uses a trained artificial intelligence model to detect and classify Country Flags.

The model was trained using the ImageNet architecture with NVIDIA's Jetson-inference library and is optimized to run efficiently on a Jetson Orin Nano.

# Image 
Here is an image of what the final product should look like produced from the AI: <img width="782" height="500" alt="Screenshot 2026-07-22 162504" src="https://github.com/user-attachments/assets/fc796155-bc5a-409c-b5e7-c116143a306a" />



# Algorithm
The algorithm is full very strong complex build coding that actually helps python and the coding to work.

[train.py](https://docs.google.com/document/d/1r1jNkRI6imb0M9-d9pJxcpGsBdCVZcB3VCT4ukZtNSU/edit?usp=sharing) is very important for training the AI to be able to recognize the variety of country flags. This is the whoel reason the AI is able to match the country flag with the country its from.


[reshape.py](https://docs.google.com/document/d/1ixoCs2YjEqiHwX1uDFOO8WvU2MSL9V-mXjy-0gXA9Pk/edit?usp=sharing) is a script that is typically used to reorganize or transform the structure, dimensions, or layout of data without changing the actual values inside it.

[voc.py](https://docs.google.com/document/d/1uEBq4bOQinJpxnPhVNyyQOaNRQvE6ZcFsqi8NskSH00/edit?usp=sharing) is a script in Python which is most commonly used in computer vision projects to handle the PASCAL VOC (Visual Object Classes) dataset.

[onnx_export.py](https://docs.google.com/document/d/11t_kcadnQTxFRAQLuW_Vp_XNlc-H9e8FWJo7Riqxud4/edit?usp=sharing) is a script is used to convert or "export" a trained deep learning model into the ONNX (Open Neural Network Exchange) format.







# Running this project
here are the following steps and requirments for the project:

## hardware for the Project:

here we have the following hardware to actually run the project:
*   NVIDIA Jetson Orin Nano
*   Jetson-inference 
*   USB Webcam which is optional for real-time inference


 ## Dataset

Next up we have the dataset. The dataset sourced from Kaggle is used for training for the project. It's has been restructured to be compatible with the classification requirements of `jetson-inference`. 

this is the dataset i used for my project: https://www.kaggle.com/datasets/shuvokumarbasak4004/world-flags-dataset-195 

The dataset is split using the file systems below:

dataset/

├── train/       # Training images

├── val/         # Validation images

└── test/        # Testing images
 
 ## Coding in vs code

 Now onto the real stuff. First you have to download the Dataset. 
<pre><code>#!/bin/bash
curl -L -o ~/Downloads/world-flags-dataset-195.zip\
  https://www.kaggle.com/api/v1/datasets/download/shuvokumarbasak4004/world-flags-dataset-195</code></pre>

Next you have to change directory.
<pre><code>
cd jetson-inference/python/training/classification/data</code></pre>

Now you have to unzip the files from your downloads. You may need to create a subfolder to store the files in depending on if the dataset comes with one or not which in this case it will be required.

<pre><code> unzip ~/Downloads/your_dataset.zip -d subfolder_name</code></pre>

And now you will organize the Dataset (test/val/train)
<pre><code>
python3 reshape.py</code></pre>



In your dataset directory create a new file named labels.txt. Once your inside labels.txt, put each country in alphabetical order. It won't work unless it is all in alphabetical order.


After you have put it all in alphabetical order run the docker container: 

<pre><code>
cd ~/jetson-inference/
./docker/run.sh</code></pre>

Navigate into your classification folder with these two commands:

<pre><code>
cd python/training/classification</code></pre>

<pre><code>
python3 train.py --model-dir=models/Your_Model data/dataset</code></pre>

And IF you want to change the training amount change the epoch= with a smaller number for shorter training and a bigger number for longer training
<pre><code>
python3 train.py --epochs=10 --model-dir=models/Your_Model data/dataset</code></pre>

Now run the ONNX export script:
<pre><code>
python3 onnx_export.py --model-dir=models/Your_Model</code></pre>

Exit the docker container with
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
