# Apply_TFLITE_in_Android
How to apply a trained Tensorflow Lite model (.tflite) in an Android application.

[image1]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/1.JPG "gradle1"
[image2]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/2.jpg "gradle2"
[image3]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/3.jpg "model1"
[image4]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/4.jpg "model2"
[image5]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/5.jpg "model3"
[image6]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/6.jpg "model4"
[image7]: https://github.com/moritzzzzz/Apply_TFLITE_in_Android/blob/master/7.jpg "model5"

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





