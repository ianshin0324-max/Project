# project
#   Country Flag Recognition

This project uses a trained artificial intelligence model to detect and classify Country Flags.

The model was trained using the ImageNet architecture with NVIDIA's Jetson-inference library and is optimized to run efficiently on a Jetson Orin Nano.


hardware for the Project:

*   NVIDIA Jetson Orin Nano
*   Jetson-inference 
*   USB Webcam which is optional for real-time inference

# Dataset

The datasets sourced from Kaggle is used for training for the project. It has been restructured to be compatible with the classification requirements of `jetson-inference`. 

The dataset is split using the file systems below:

dataset/

├── train/       # Training images

├── val/         # Validation images

└── test/        # Testing images
