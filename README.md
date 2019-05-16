# Apply_TFLITE_in_Android
How to apply a trained Tensorflow Lite model (.tflite) in an Android application.

## Motivation
Training neural networks for use in AI agents is fun, but having them run on a VM, far from where their use can be applied is boring. Therefore running the trained models for prediction inside mobile applications makes sense. 

Here I will show how I implement a TensorFlowLite model (.tflite) in an Android application, for the task of image recognition.

## Preparing the Android application for TFLite

First thing we need to do is prepare the Android gradle file, in order to tell Android, not to compress the model, which would kill it, as the weights might slightly change through compression.


