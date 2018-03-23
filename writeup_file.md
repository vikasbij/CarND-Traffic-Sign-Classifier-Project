
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
# [//]: # (Image References) 

[image1]: ./examples/visualization.jpg [image2]: ./examples/grayscale.jpg "Grayscaling" [image3]: ./examples/random_noise.jpg "Random Noise" [image4]: ./examples/placeholder.png "Traffic Sign 1" [image5]: ./examples/placeholder.png "Traffic Sign 2" [image6]: ./examples/placeholder.png "Traffic Sign 3" [image7]: ./examples/placeholder.png "Traffic Sign 4" [image8]: ./examples/placeholder.png "Traffic Sign 5"

[image1]: ./examples/visualization.jpg "Visualization" [image2]: ./examples/grayscale.jpg "Grayscaling" [image3]: ./examples/random_noise.jpg "Random Noise" [image4]: ./examples/placeholder.png "Traffic Sign 1" [image5]: ./examples/placeholder.png "Traffic Sign 2" [image6]: ./examples/placeholder.png "Traffic Sign 3" [image7]: ./examples/placeholder.png "Traffic Sign 4" [image8]: ./examples/placeholder.png "Traffic Sign 5"

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

# Data Set Summary & Exploration # ### Data Set Summary & Exploration 

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

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the image to a grayscale image because it reduces time taken in processing as the image is monotonous rather than having 3 layers which is more time consuming and even it takes longer to make predictions.
The grayscale pixel intensities are unsigned integer values, with the values of the pixels falling in the range (0,255).

Then, I normalized the image data because wider distribution of data makes it more difficult to train by single learning rate.So, after normalization, with different features having different ranges weight can be diverged by single learning rate.

Original image set:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture1.PNG)

Output after preprocessing:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Report_Images/Capture2.PNG)

#  Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

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


# Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

While training the LeNet Architecture I modified the following values for the hyperparameters:

Epochs = 20

Batch_size = 138

Adam Optimizer with Learning rate = 0.00097

I changed the epochs, batch size and learning rate. Before deciding to keep it this way and on further modifications i achieved test accuracy of around 94.4

#  Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem. 

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

# Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

The model correctly guessed 8 of the 10 traffic signs,hence giving an accuracy of 80%.

# Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

shown below is the image of output predicted for the web images:


Image 1:

![img1](https://github.com/vikasbij/CarND-Traffic-Sign-Classifier-Project/blob/master/Images_test/1.jpg?raw=true)

Label1: Stop = 1.0000000e+00
Label2: End of all speed and passing limits = 1.1445986e-18
Label3: No entry = 1.1745871e-20
Label4: Keep right = 3.768698948834054e-13
Label5: Turn left ahead = 1.5403739e-24
       

Image 2:
Bumpy road

Label1: Bumpy road = 1.0000000e+00
Label2: Bicycles crossing = 6.0424854e-10
Label3: Yield = 2.4987214e-15
Label4: Children crossing = 2.1285474e-15
Label5: Road work = 6.0802021e-16


Image 3:
Speed limit (50km/h)

Label1: Speed limit (50km/h) = 9.2261392e-01
Label2: Speed limit (100km/h) = 7.4616611e-02
Label3: Speed limit (80km/h) = 2.6664478e-03
Label4: Speed limit (70km/h) = 4.8524205e-05
Label5: Speed limit (30km/h) = 4.7358575e-05

Image 4:
Road work

Label1: Right-of-way at the next intersection = 1.0000000e+00
Label2: Dangerous curve to the right = 3.0683314e-11
Label3: Beware of ice/snow = 4.1066445e-13
Label4: Slippery road = 1.2038996e-15
Label5: Vehicles over 3.5 metric tons prohibited = 7.1423678e-17


Image 5:
Speed limit (70km/h)

Label1: Speed limit (30km/h) = 5.5248260e-01
Label2: Stop = 4.2263725e-01
Label3: Speed limit (120km/h) = 8.2846079e-03
Label4: Speed limit (70km/h) = 6.6708126e-03
Label5: End of all speed and passing limits = 2.1819612e-03


Image 6:
Roundabout mandatory

Label1: Roundabout mandatory = 9.9997973e-01
Label2: No passing = 1.9577465e-05
Label3: End of all speed and passing limits = 2.9338540e-07
Label4: Priority road = 1.5697889e-07
Label5: Vehicles over 3.5 metric tons prohibited = 8.0206256e-08       

Image 7:
No entry

Label1: No entry = 9.9710566e-01
Label2: Stop = 2.8943052e-03
Label3: Turn right ahead = 4.4485740e-10
Label4: Turn left ahead = 3.3688782e-10
Label5: Speed limit (120km/h) = 2.2270920e-10


Image 8:
Turn left ahead

Label1: Turn left ahead = 9.9710566e-01
Label2: Right-of-way at the next intersection = 2.8943052e-03
Label3: Beware of ice/snow = 4.4485740e-10
Label4: No entry = 3.3688782e-10
Label5: Vehicles over 3.5 metric tons prohibited = 2.2270920e-10


Image 9:
Wild animals crossing 

Label1: Wild animals crossing = 1.0000000e+00
Label2: Double curve = 5.7172989e-14
Label3: Slippery road = 2.1863365e-21
Label4: Road work = 1.1732914e-30
Label5: Speed limit (50km/h) = 2.4616694e-32


Image 10:
Right-of-way at the next intersection

Label1: Right-of-way at the next intersection = 1.0000000e+00
Label2: Beware of ice/snow = 7.5917102e-24
Label3: Pedestrians = 3.8036297e-24
Label4: Vehicles over 3.5 metric tons prohibited = 2.5203890e-27
Label5: Double curve = 3.2053543e-28

The forth and the fifth images were not identified correctly as the image for an right-of-way at the next intersection 
looks similar to that of Road work and similarly for the other, when an image of 32*32 is used and the image gets low in 
resolution when converted to gray scale and normalization is applied thus it almost looks similar to 
output class predicted by the model.
