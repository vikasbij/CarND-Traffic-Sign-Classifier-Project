
# # **Traffic Sign Recognition**

# Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer. 

**Build a Traffic Sign Recognition Project**
# The goals / steps of this project are the following: 
* Load the data set (see below for links to the project data set) 
* Explore, summarize and visualize the data set 
* Design, train and test a model architecture 
* Use the model to make predictions on new images 
* Analyze the softmax probabilities of the new images 
* Summarize the results with a written report



[image1]: ./examples/visualization.jpg "Visualization" 
[image2]: ./examples/grayscale.jpg "Grayscaling" 
[image3]: ./examples/random_noise.jpg "Random Noise" 
[image4]: ./examples/placeholder.png "Traffic Sign 1" 
[image5]: ./examples/placeholder.png "Traffic Sign 2" 
[image6]: ./examples/placeholder.png "Traffic Sign 3" 
[image7]: ./examples/placeholder.png "Traffic Sign 4" 
[image8]: ./examples/placeholder.png "Traffic Sign 5"

# ## Rubric Points

### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation

# ### Writeup / README 

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.    

# Data Set Summary & Exploration

#  Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic signs data set: 
 
Number of training examples = 34799


Number of testing examples = 12630

Image data shape = (32, 32, 3)

Number of classes = 43

# Include an exploratory visualization of the dataset.

Here I have plotted an exploratory visualization of the dataset. Shown below is the bar chart visualization of validation,training abd test data:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture4.PNG)

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture3.PNG)

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture5.PNG)

# Design and Test a Model Architecture


As a first step, I decided to convert the image to a grayscale image because it reduces time taken in processing as the image is monotonous rather than having 3 layers which is more time consuming and even it takes longer to make predictions.
The grayscale pixel intensities are unsigned integer values, with the values of the pixels falling in the range (0,255).

Then, I normalized the image data because wider distribution of data makes it more difficult to train by single learning rate.So, after normalization, with different features having different ranges weight can be diverged by single learning rate.

Original image set:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture1.PNG)

Output after preprocessing:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture2.PNG)

# model architecture

My final model layer description :

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Grayscale image						| 
| Convolution 5x5     	| 2x2 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, outputs 14x14x6	 				|
| Convolution 5x5	    | 2x2 stride, valid padding, outputs 10x10x16	|
| RELU					|												|
| Max pooling	      	| 2x2 stride, outputs 5x5x16	 				|
| Convolution 1x1		| 2x2 stride, valid padding, outputs 1x1x412	|
| RELU					|												|
| Fully connected		| input 412, output 122							|
| RELU					|												|
| Dropout				| 												|
| Fully connected		| input 122, output 84							|
| RELU					|												|
| Dropout				| 												|
| Fully connected		| input 84, output 43							|


# training of model

While training the LeNet Architecture I modified the following values for the hyperparameters:

Epochs = 20

Batch_size = 138

Adam Optimizer with Learning rate = 0.00097

I changed the epochs, batch size and learning rate. Before deciding to keep it this way and on further modifications i achieved test accuracy of around 94.4

#  My approach taken for finding a solution and getting the validation set accuracy 

In my final model output I was able to achieve:

• training set accuracy of 99.9% 

• validation set accuracy of 95.5% 

• test set accuracy of 94.4%
    

If an iterative approach was chosen:

• What was the first architecture that was tried and why was it chosen?

LeNet architecture was used,it would be similar architecture offered to us. Itwas easy to understand and has given me a good score.

• What were some problems with the initial architecture?

Lack of data and lack of knowledge of other parameters. Adding few convolution layers and further playing with the hyperparameters helped me reaching higher accuracy.

• How was the architecture adjusted and why was it adjusted? 

It was adjusted by adding a few convolution layers and a couple dropouts to the previous architecture as it was not able to achieve the desired accuracy.

• Which parameters were tuned? How were they adjusted and why?

o Epoch: I played around with this and set it to 20 as I was able to achieve good value for accuracy. 
o I increased the batch size as learned we can increase the data size if memory allows it . 
o The learning rate I think could have been left at .001 as it was default good rate by I tried changing it as it mattered a little  

• What are some of the important design choices and why were they chosen?

The original LeNet architecture used TANH,the reason we use RELU as it gives better classification accuracy due to a number desirable properties Convolution preserves the spatial relationship between pixels by learning image features using small filter square over the input data.These filters acts as feature detectors from the original input image.The more number of filters we have, the more image features get extracted and the better our network becomes at recognizing patterns in unseen images.

It provide me with such learning opportunity that I could take weeks more to learn. I could still learn more about that. I think the  thing I learned was having a more uniform dataset along with enough convolutions to capture features will improve speed of training and accuracy.

# Test a Model on New Images

Following are the 10 German traffic signs that I reffered on web:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture8.PNG)

Some of the images might be misclassified by the model due to high level of similarities such as traffic signs enclosed inside same boundary figure like triangle, circle and posses almost similar characterstc like color.
This may also vary due to poor lighting condtions as two images may look similair to some extent under extreme or poor lighting. 

# Model Prediction:

The model correctly guessed 8 of the 10 traffic signs,hence giving an accuracy of 80%.

Here is the result of the prediction of the images:

| Image			        				|     Prediction	        			| 
|:-------------------------------------:|:-------------------------------------:| 
| Stop sign      						| Stop sign   							| 
| Bumpy Road     						| Bumpy Road							|
| Speed limit (50 km/h)					| Speed limit (50 km/h)					|
| Road work								| Road work								|
| Right-of-way at the next intersection	| Road work								|
| Speed limit (70 km/h)					| Speed limit (30 km/h)					|
| Roundabout mandatory					| Roundabout mandatory					|
| No entry	      						| No Entry 						 		|
| Turn left ahead						| Turn left ahead      					|
| Wild animals crossing 				| Wild animals crossing					|

# Model Prediction for top 5 softmax

shown below is the image of output predicted for the web images:


Image 1:

Stop sign

| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 1.0         				| Stop sign   									| 
| 1.1445986e-18				| End of all speed and passing limits			|
| 1.1745871e-20				| No entry										|
| 3.768698948834054e-13		| Keep right 					 				|
| 1.5403739e-24			   	| Turn left ahead      							|


Image 2:
Bumpy road

| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 1.0000000e+00				| Bumpy road   									| 
| 6.0424854e-10				| Bicycles crossing								|
| 2.4987214e-15				| Yield											|
| 2.1285474e-15				| Children crossing				 				|
| 6.0802021e-16   			| Road work			 							| 



Image 3:
Speed limit (50km/h)

| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 9.2261392e-01				| Speed limit (50km/h)   						| 
| 7.4616611e-02				| Speed limit (100km/h)							|
| 2.6664478e-03				| Speed limit (80km/h) 							|
| 4.8524205e-05				| Speed limit (70km/h)			 				|
| 4.7358575e-05			   	| Speed limit (30km/h)							| 

Image 4:
Road work

| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 1.0000000e+00				| Right-of-way at the next intersection 		| 
| 3.0683314e-11				| Dangerous curve to the right					|
| 4.1066445e-13				| Beware of ice/snow							|
| 1.2038996e-15				| Slippery road					 				|
| 7.1423678e-17			   	| Vehicles over 3.5 metric tons prohibited 		|


Image 5:
Speed limit (70km/h)

| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 5.5248260e-01				| Speed limit (30km/h)  						| 
| 4.2263725e-01				| Stop											|
| 8.2846079e-03				| Speed limit (120km/h)							|
| 6.6708126e-03				| Speed limit (70km/h)			 				|
| 2.1819612e-03			   	| End of all speed and passing limits			| 



Image 6:
Roundabout mandatory


| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 9.9997973e-01				| Roundabout mandatory   						| 
| 1.9577465e-05 			| No passing									|
| 2.9338540e-07 			| End of all speed and passing limits			|
| 1.5697889e-07 			| Priority road					 				|
| 8.0206256e-08   			| Vehicles over 3.5 metric tons prohibited		| 


Image 7:
No entry

| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 9.9710566e-01				| No entry   									| 
| 2.8943052e-03				| Stop											|
| 4.4485740e-10				| Turn right ahead								|
| 3.3688782e-10				| Turn left ahead    				 			|
| 2.2270920e-10				| Speed limit (120km/h) 						| 


Image 8:
Turn left ahead


| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 9.9710566e-01				| Turn left ahead 								| 
| 2.8943052e-03				| Right-of-way at the next intersection			|
| 4.4485740e-10				| Beware of ice/snow							|
| 3.3688782e-10				| No entry    				 					|
| 2.2270920e-10				| Vehicles over 3.5 metric tons prohibited 		|


Image 9:
Wild animals crossing


| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 1.0000000e+00				| Wild animals crossing							| 
| 5.7172989e-14				| Double curve									|
| 2.1863365e-21				| Slippery road									|
| 1.1732914e-30				| Road work    				 					|
| 2.4616694e-32				| Speed limit (50km/h)					 		|


Image 10:
Right-of-way at the next intersection


| Probability         		|     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 1.0000000e+00				| Right-of-way at the next intersection			| 
| 7.5917102e-24				| Beware of ice/snow							|
| 3.8036297e-24				| Pedestrians									|
| 2.5203890e-27				| Vehicles over 3.5 metric tons prohibited  	|
| 3.2053543e-28				| Double curve					 				| 

The images right-of-way at the next intersection and Speed limit (70 km/h) are not identified correctly as the image for an right-of-way at the next intersection 
looks similar to that of Road work both are traingular images coloured with blue boundaries so the neural network may be classifying it to be similar to that of Road work and similarly for Speed limit (70 km/h) image have same characterstics in shape and color as that of Speed limit (30 km/h) and hence may be wrongly classified. 
Also when an image of 32*32 is used and the image gets low in 
resolution when converted to gray scale and normalization is applied thus it almost looks similar to 
output class predicted by the model.
