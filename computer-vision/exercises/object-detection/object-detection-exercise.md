# Exercise: Build An Object Detection Solution

## Introduction

You have now learned about the capabilities of the Custom Vision service and how it can be used to create custom object detection models using images you provide. The object detection demo walked through how to use the Custom Vision portal to build, train, test and deploy an object detection model, and now it is time for you apply what you have learned.

In this exercise, you use the Azure Custom Vision service train a custom object detection model, and then deploy the model to a prediction service for consumption. You will then use a Jupyter notebook in Azure Machine Learning Studio to send images into your prediction service for detecting entities within those images and examine the results.

## Requirements

- You must have an Azure subscription to complete this exercise. If you don't have one, you can sign up for a free trial at <https://azure.microsoft.com/free>.
- You will not be using a Udacity workspace to complete this exercise.
- You must have completed the Exercise Resource Setup in order to complete this exercise.

## Instructions

TODO: Reference this: https://docs.microsoft.com/en-us/learn/modules/detect-objects-images-custom-vision/3-create-object-detection-solution

After completing all of the tasks outlined in the Exercise Resource Setup guide, complete that tasks listed below to create, train, test, and publish a custom object classification model. Then, follow the steps within the indicated Jupyter notebook to consume the deployed model using Python code.

_Task list_

- Open a web browser and navigate to the [Computer Vision portal](https://www.customvision.ai/). Sign in using the account associated with your azure subscription.
- In the Custom Vision portal, open a new `Object detection` project named `XXX`. Make sure to associate the project with your Custom Vision training resource and use the `General` domain.
- Upload and tag the images located in `IMAGE_FOLDER`.
- Train the model.
- Test the model using the images located in `TEST_IMAGE_FOLDER`.
- Publish the model to your Custom Vision's prediction resource.
- Retrieve the keys for your prediction resource.
- Retrieve the `Project Id` for your deployed object detection model.
- Open [Azure Machine Learning Studio](https://ml.azure.com/), locate the `udacity-ml-vm` compute you created during the exercise resource setup, and open its associated `Jupyter` environment.


- Return to the Jupyter environment window and open the `lesson-computer-vision-read-text.ipynb` notebook in the `udacity-ai-fundamentals/lesson-computer-vision` folder and follow the instructions within the notebook to complete the rest of the exercise. Note, you may need to hit refresh on the window to see the `udacity-ai-fundamentals` folder.
