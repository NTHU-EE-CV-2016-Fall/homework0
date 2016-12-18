# Your Name <span style="color:red">(104061563)</span>

#Project 4 / Face Detection with a Sliding Window

## Overview
The project is related to face recognition
> In this project, we apply Dalal and Bill Triggs' method to perform face detection. The method is that: (1) Compute the HOG features of head photos as positive features and HOG features of non-face photos as negetive features. (2) train the parameters using LSVM (3) finally use the trained LSVM to determine faces in test images using scaled sliding window.

> Tunable parameters:
(1)num_negative_examples
(2)feature_params.hog_cell_size
(3)SVM->lambda
(4)run_detector->thrld
## Data explanation
10524 36*36 face images
275 different sizes non-face images(tree,mountain...etc)
130 gray scale test images
5 extra test figures

## Implementation
1. Positive and negetive features
	* Positive features: compute HOG features with HOG cell size 6 and with input 36*36 face images
	* Negetive features: Use sliding window to intercept 36*36 window images from non-face images.(This step will generate over 10000 of features, we made a threshlod to limit the amount of features to enhance our speed)
2. LSVM
	* use function: 'vl_svmtrain' to train 1116 dimension parameters which will then be used to classify between the face and non-face images.
<<<<<<< HEAD
3. Examine learned classifier:
	* loop over lambda=[0.1 0.001 0.0001 0.00001] and num_negative_examples(amount of non_face examples to train), and we get it reaches highest true positive score of 0.401(lowest false positive), whose confusion matrix looks like this:
=======
3. Examin learned classifier:
	* loop over lambda=[0.1 0.001 0.0001 0.00001] and num_negative_examples(amount of non_face examples to train), and we get it reaches highest true positive score of 0.397(lowest false positive), whose confusion matrix looks like this:
>>>>>>> origin/master

<img src="confusion_m.jpg" width="80%"/>
	* confidence plot:
<img src="confidences.jpg" width="80%"/>
	this plot shows that some positive pictures are classified to non-face in train set and the vise versa.
	* Visualize our learned detector
<img src="hog_template.jpg" width="80%"/>
we can roughly see a face in it.

4. Detect faces in the test images
	* Multiscale, sliding windows are used in the detect method. 
	* Multiscale: calculate HOG features under different Hog cell size
	* Sliding window: search every 6*6 subimage in every test images with a window, the window size should be the same as the training window.
	
```
Code highlights
```

## Installation
* VL_feats
http://www.vlfeat.org/download.html

### Results

<table border=1>
<tr>
<td>
<img src="photo/1.jpg" width="24%"/>
<img src="photo/2.jpg"  width="24%"/>
<img src="photo/3.jpg" width="24%"/>
<img src="photo/4.jpg" width="24%"/>
</td>
</tr>

<tr>
<td>
<img src="photo/5.jpg" width="24%"/>
<img src="photo/6.jpg"  width="24%"/>
<img src="photo/7.jpg" width="24%"/>
<img src="photo/8.jpg" width="24%"/>
</td>
</tr>

</table>


<center>
<p>
Face template HoG visualization for the starter code. This is completely random, but it should actually look like a face once you train a reasonable classifier.
Precision Recall curve for the starter code.
<p>
<img src="AP.jpg">
<p>
Example of detection on the test set from the starter code.
<img src="detections_Argentina.jpg">

</center>
