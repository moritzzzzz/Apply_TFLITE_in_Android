# Apply_TFLITE_in_Android
How to apply a trained Tensorflow Lite model (.tflite) in an Android application.

[image1]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/1.JPG "gradle1"
[image2]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/2.jpg "gradle2"
[image3]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/3.jpg "model1"
[image4]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/4.jpg "model2"
[image5]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/5.jpg "model3"
[image6]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/6.jpg "model4"
[image7]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/7.jpg "model5"
[image8]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/8.jpg "model6"
[image9]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/9.jpg "model7"
[image10]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/10.jpg "model8"
[image11]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/11.jpg "model9"

## Motivation
Training neural networks for use in AI agents is fun, but having them run on a VM, far from where their use can be applied is boring. Therefore running the trained models for prediction inside mobile applications makes sense. 

Here I will show how I implement a TensorFlowLite model (.tflite) in an Android application, for the task of image recognition.

## Preparing the Android application for TFLite

First thing we need to do is prepare the Android gradle file, in order to tell Android, not to compress the model, which would kill it, as the weights might slightly change through compression.

![Gradle1][image1]

Load TFLite libraries:

![Gradle2][image2]

## Put the model into the resources

The model file needs to be put into a folder of type "Assets". if it does not yet exist, create such a folder under resources (res):

![Model1][image3]

Place the trained model, of format .tflite, into this assets folder.

## Hints for building the Android Activity 

The Android activity is the actual java class that will run the trained TFLite model. Therefore we need to import the TFLite interpreter:

![Model2][image4]

### Load model file

This method will load the TFLite model:

![Model3][image5]

Calling the method, to load the model into the TFLite interpreter:

![Model4][image6]

### If activity is a service
Change "Activity" to "Context" in LoadModel():

![Model5][image7]

## Preprocessing: Input data pipeline

At this point, we have to prepare our input data for processing by the TFLite model. As I have mentioned, this example discusses processing image input data. Therefore we need to preprocess the input image, to fit the input layer of the trained neural network.

In my case the input layer of the neural network is of dimensions 224x224x3. (quadratic RGB image with 224 pixels side length)
Below method will crop a region of size 224x224 out of a larger image, as this is the region of interest:

![Model6][image8]

The cropped image now fits the input layer dimensions.

### Image operations

**Run the image operations, as well as the prediction in an asynchronous task, as these operations are CPU/GPU intensive. This will create a new CPU/GPU thread and not slow down the UI Thread**

The TFLite interpreter takes either a ByteBuffer or a FloatBuffer as input, no bitmap. For that we need to convert the RGB bitmap to one of these formats. 

In below function we will iterate over the RGB pixel values with 2 for-loops and will write the pixel values into the ByteBuffer:

![Model7][image9]

### Executing the prediction

My model is trained to recognize humans, nothing else. Therefore my output is a single probability. In below result assignment, only the first element of the output array is required:

![Model8][image10]

![Model9][image11]





