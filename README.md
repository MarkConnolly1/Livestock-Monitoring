#Determining the best Computer Vision model for a Livestock monitoring system with behavioural analysis

I am currently working on my final year project, where I am applying Computer Vision and training You Only Look Once (YOLO) models to monitor livestock and analyse their behaviour. The objective is to develop a reliable system capable of detecting various behaviours in different environments to assist in better management and care. I am training and evaluating the performance and accuracy of two versions of the YOLO object detection models: YOLOv5 and YOLOv7. This system aims to provide insights into livestock health and behaviour, facilitating proactive management and improved welfare practices.

# YOLO (You Only Look Once)
The YOLO (You Only Look Once) model is a powerful deep learning algorithm used for object detection in images and videos. Unlike traditional object detection systems which apply a classifier to different parts of an image multiple times, YOLO frames object detection as a single regression problem, straight from image pixels to bounding box coordinates and class probabilities. This approach allows YOLO to detect objects in images in real-time, achieving high speeds and accuracy with a single forward pass of the network.

# Setup/What you will need
- Conda Enviroment

- Python 3.8 or later

# Clone the YOLOv5 Repository

- !git clone https://github.com/ultralytics/yolov5

![Screenshot 2024-03-20 130806](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/f7ec5eef-2219-4ece-a2e4-ac917fdb0ce5)

- %cd yolov5
  
- %pip install -r requirements.txt
  
# How To Train Your Model

To train a YOLO model using your dataset, follow this command template. Substitute the placeholders with the specific location of your dataset, the model weights file you want to use, the desired number of training epochs.

- python train.py --img 640 --batch (ENTER BATCH SIZE - 16 IS RECOMMENDED) --epochs (ENTER NUMBER OF EPOCHS YOU WANT TO TRAIN) --data (LINK TO YOUR DATA.YAML FILE) --weights yolov5s.pt

  - Batch Size - refers to the number of training samples used to train the model in one iteration (or one forward and backward pass). In each iteration, the model weights are updated based on the gradient of the error with respect to the batch.The choice of batch size can significantly influence the training dynamics. A smaller batch size often leads to a more stable convergence, but at the cost of increased computation time, as more updates are needed. A larger batch size can speed up the training process due to better utilization of hardware (like GPUs), but might lead to a less stable convergence. The recommended size of 16 is a balance of both which is what I decided to utilize when training my models.
    
  - Epochs - An epoch is one complete cycle through the entire training dataset. This parameter specifies how many times the training process should iterate over the entire dataset. More epochs can potentially lead to a better-trained model as it gets more opportunities to learn from the entire data. However, training for too many epochs can also lead to overfitting. For the lighter YOLO models I did over 40 epochs but for the bigger models such as YOLOv7 (2 epochs trained) and YOLOv5l (1 epoch trained) This was due to computation power and trying stay on the projects timeline.
 
  -  Image Size -  Image size directly affects the amount of information available to the model for detecting objects. Larger images provide more detailed information which can improve detection accuracy but also require more computational power and memory, potentially slowing down training. Smaller images train faster but might lack essential details, leading to poorer model performance. 640 x 640 was the recommened image size for the YOLO models so I decided to use that.

  
![Screenshot 2024-03-26 012900](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/8b07f791-789e-4e75-b53f-220ea33a605d)
![Screenshot 2024-03-26 155036](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/c21814eb-e7fd-47eb-a5ad-511a5aca99ea)
![Screenshot 2024-03-25 143957](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/2f9ab945-13ba-4877-97ac-bc95f8eaa0cd)


# How To Detect
Once the model is successfully trained, you can apply the trained weights to detect objects in new images or videos. To do this, follow the detect command below.

-python detect.py --weights best.pt --img 640 --conf 0.25 --source (/path/to/images_or_video)

  - Confidence Threshold - This parameter specifies the minimum confidence level for the model to consider a detection as valid. Confidence, in this context, is a measure of the model's certainty that a detected object belongs to a specific class. The confidence value is crucial in filtering out detections that the model is uncertain about. The value of the confidence threshold can range from 0 to 1 The confidence value in this command was set to 0.25  which means any objects detected with a confidence value of 25 or more is considered valid.

![Screenshot 2024-04-16 140012](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/6211afe9-7333-458c-8ff4-85af7a7023c0)
![Screenshot 2024-04-12 104410](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/0f169071-4416-44a6-9ab0-c43478faee32)
![Screenshot 2024-04-16 142958](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/cab8721e-53c1-4b0d-a08e-e003a65beec6)
![Screenshot 2024-04-16 143017](https://github.com/MarkConnolly1/Livestock-Monitoring/assets/121117520/2c61d4c5-e1b1-499e-9459-b875d96b29be)


