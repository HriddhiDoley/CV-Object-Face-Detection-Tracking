# CV-Object-Face-Detection-Tracking
Computer Vision Program to detect object and face, smile, eyes and track it

![image](https://github.com/user-attachments/assets/c5666492-9882-47ad-88a8-630b77ac08a8)

## About the input video 
The short video recorded is aligned with the list of MS COCO class names. The video is 13s long and it is in .mp4 format
There are 6 objects some of them are moving and some are static 
* Moving objects: Person, Sports Ball, Hat.   
* Static objects: Cup, Book, Teddy Bear.
Due to its shape, size, and color, the hat was detected as a cake in some frames and as a frisbee in others. As this object was not correctly identified, it is not part of the evaluation below. 
The video is clear with good lighting. Although in some frames the moving objects are blurry due to the fast motion.

## Ground Truth
Ground Truth is prepared using a tool called Computer vision Annotation Tool(CVAT). The Output of CVAT is in .xml format and the below code extracts the frame, object ID and the bounding boxes and export into a .csv file for future evaluation.

## Task1 & Task 2:  Object Tracking and Recognition
* The model used for object detection is a pre-trained Mask R-CNN
* Objects are detected frame-by-frame in the video (task1.mp4)
* Association method IoU is used to unique object IDs and track the objects
* Bounding Boxes and labels are drawn on the output video (task2.mp4) showing which object ID corresponds to which ID, with labels and scores.
* A confidence threshold of 0.5 is used to filter out low-confidence predictions.

## Task 3: The faces, eyes, and smiles of the person were detected, and the face object was tracked. 
* Haar Cascades: Three different pre-trained Haar Cascade classifiers are loaded : 
  * haarcascade_frontalface_default.xml for face detection
  * haarcascade_eye.xml for detecting eyes
  * haarcascade_smile.xml for detecting smiles.
* Face Detection: For each frame, faces are detected using face_cascade.detectMultiScale(). This function returns the coordinates of the bounding boxes around the detected faces.
* Eye and Smile Detection: Inside each detected face, detect eyes and smiles, and draw corresponding bounding boxes inside the face region.
* Face Tracking: Detected faces are tracked across frames using IoU-based matching, associating each face with a unique ID.
* Bounding Box Drawing: Bounding boxes are drawn around detected faces, eyes, and smiles. The ID of each tracked face is displayed above the face bounding box.
* CSV Logging: The face tracking information (frame number, object ID, bounding box coordinates) is logged to a CSV file (face_detection_results.csv).
* Output Video: The video with overlaid face detection results is saved as task3.mp4.

## Evaluation method: 
* A .csv file (object_tracking_results.csv) is also generated to capture the frame, object ID and bounding boxes coordinates for the detected objects.
* The Output of CVAT is in .xml format and the below code extracts the frame, object ID and the bounding boxes and export into a .csv file (groundtruth.csv) for evaluation.
* Comparison of Ground Truth and Detected object/ faces
    * The association method of IoU is used to compute the intersection over union between two bounding boxes. 
    * For each object in the ground truth, we check if there is a corresponding detected face in the same frame with an IoU greater than or equal to the threshold (0.5 in this case).
    * If a match is found, it's counted as a true positive.
    * If no match is found, it’s counted as a false positive.
* Evaluation Metrics: 
    * True Positive (TP): Correctly detected faces/objects.
    * False Positive (FP): Detected faces/objects that don’t correspond to any ground truth face/object.
    * False Negative (FN): Faces/objects in the ground truth that were not detected.
    * Precision: Proportion of detected faces/objects that are correct.
    * Recall: Proportion of actual faces/objects that were detected.
    * F1-Score: The harmonic mean of precision and recall, representing the balance between both.

The evaluation results and analysis of the face and object detections and tracking tasks are as follows: 
![image](https://github.com/user-attachments/assets/13e13188-4158-4ef9-aef0-105d53ecd571)
![image](https://github.com/user-attachments/assets/ab2cdeb5-0962-42be-a311-7b296fc11c0e)
![image](https://github.com/user-attachments/assets/7dae9b3c-aff1-441d-a0d3-59f4468f22e2)


