# OBJ-Detection
Object detection Theory
---
Resource - https://www.youtube.com/watch?v=9I6nzfx_kpE&list=PL1GQaVhO4f_jLxOokW7CS5kY_J1t1T17S

- Faster RCNN, RFCN, YOLO, SSD
---

Evaluating ML Models 
- Precision/recall F1 Calculations -
- we need F1 score which is combination of both - Precision + Recall
- if both are high you will get high f1 score.
- what recall does is ? It tried to filter out if correct label is assigned or not out of total number of correct labels.
- lets see this later on

---

# Object Detection -
- classification classify the object by softmax scores
- localization will tell us about -> where the object is located
- Object detection would tell us where all objects are located - multi-objects

- Conv + Pool layers would act as Feature Extractors
- Fully connected acts as Classification.
- Classical CV used - SIFT/ HOG and SVM as classifier
- Modern CV uses CNN Feature extractor - FC + Softmax as Classifier.
- softmax takes final layer in FC and convert it into probabilities.
- 

![image](https://github.com/user-attachments/assets/c5ac4de2-1891-4749-b124-53198a3d2a82)

### Lets see how can we modify the classification pipeline to do ->  Localization ?
- localization has 1 object in the image.
- to draw bounding box we either need 2 points / one centre point with width, height.
- In classifocation, we get class scores by using Softmax.
- now, how can we modify the last FC to give us 4 points, which presents co-ordinates of Boudning box.
- last layer FC is giving us one score / class -> to localize the object we need 4 scores
- we get bounding boxes using L2 Loss
- will modify the last layer, to give us 4 scores.
- so will have 4 scores per each class in detection pipeline - we can train the network to give me - 4 values using L2 loss
- we wont use any softmax here, as we need actual values, no activation layer is used in regression.
- Initially, High dimensioanl FM is convrted into 1D flatten vector, and FC are initialized as 0.1 value some random value initially.
- here, as givem we take L2 loss which penalizes the error more than L1 loss.

![image](https://github.com/user-attachments/assets/4eb21612-5204-4063-9b99-53651da08a03)



- as you can see in the image, backpropogate all the losses through fully connected layer.
- L2 loss, and uodate the bounding box co-ordinates
- initially I will get random values of Bounding box, but in the end I will get correct values through back propogation.

![image](https://github.com/user-attachments/assets/92f12abf-1281-40dd-a63a-72557ffc42ca)

![image](https://github.com/user-attachments/assets/d8a444a4-8c01-4cdb-87fa-a302e1e7a98d)

- combining classifier + BBox regressor
- conv part acting as feature extractors -> classifier head + regression head
- same Feature extractor CNN can be used for both, no need to have seperate one.
- Feature extractors act as generic layer for both
- same feature map is sufficient to train and infer the BBox
- How to combine results of - Classification with its corresponding BBox
- check the conf score and thier corresponding BBox co-ordinates
- we will get the BBox co-ordinates also for other objects with low conf scores
- hence, we discard the scores with less conf score
- CNN requires fixed size input, vgg/ alexnet with 224 and 224 as input size
- 


![image](https://github.com/user-attachments/assets/42e0c507-6d2f-4330-bace-3cf2477ea4a5)


### now we know how to do localization, lets learn more about - Object Detection

- sliding window approach - we resized the image, cropped it using sliding window.
- 

![image](https://github.com/user-attachments/assets/41f10de6-56a6-430a-b700-5d2da220a61a)

- sliding window + Image pyramid
- with 6 different scales of the image, we get smaller objects as well as bigger objects
-  in big image - we can detect smaller objects
-  while in small image frame, we can detect larger objects
-  as we scale down the image, we can detect larger objects
-  sliding window resolves - location problem while image pyramid resolve the issue of - scale.
-  This pre-processing is required at the input side
-  we had ro feed images in 6 different scale.
-  CNNs take lot of time and consumes good amount of time. Its computationally expensive
-  
  
![image](https://github.com/user-attachments/assets/8bc023fd-31c5-4545-ae47-b06216b95677)

![image](https://github.com/user-attachments/assets/bcfd1ce7-6f8f-48e3-b845-6593ec7d8a07)

![image](https://github.com/user-attachments/assets/4220a65f-9fb6-4caa-bf02-f53c1326efca)

### lets solve the problem of detection 
- as we can see there are too many inputs to the CNN network, its computationally expensive process.
- 
























