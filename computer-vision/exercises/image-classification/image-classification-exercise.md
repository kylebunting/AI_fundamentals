# Exercise: Create An Image Classification Solution

## Introduction

You have now learned about the capabilities of the Computer Vision service and how it can be used to create metadata and categorize images. In many business cases, organizations need to take things one step further and using images of their own to train a machine learning model. Often, companies do not have data scientists or the amount of data required to build, train and custom machine learning models. Azure Custom Vision was created for this scenario. With Custom Vision, you can use the Computer Vision machine learning models developed by Microsoft and train them with images you provide, giving you the best of both worlds.

In this exercise, you will create a Custom Vision service in Azure, provide it multiple images to train a classification model, and then deploy the model to a prediction service for consumption. You will then use a Jupyter notebook in Azure Machine Learning Studio to send images into your prediction service for classification and observe the results.

## Requirements

- You must have an Azure subscription to complete this exercise. If you don't have one, you can sign up for a free trial at <https://azure.microsoft.com/free>.
- You will not be using a Udacity workspace to complete this exercise.

## Instructions

Follow the step-by-step instructions below to create the required resources in Azure, train an image classification model, publish the trained model to a prediction service, and consume the deployed model from a Jupyter notebook using Python code.

> **Note**: All the Azure resource used for this exercise should be created in the same region to minimize egress charges and network latency.

## Step 1: Create Custom Vision resources in the Azure portal

In this step, you create the Azure resources required to complete this exercise.

### Task 1: Create a resource group

In this task, you create a resource group in Azure, which acts as a hosting container for the various resources needed to create an image classification solution.

1. Open a web browser, navigate to the [Azure portal](https://portal.azure.com/), and sign in using the account associated with your Azure subscription.

2. On the home page of the Azure portal, select **Resource groups** under the Azure services heading.

    ![Resource groups is highlighted under the Azure services header on the Azure home page.](media/resource-groups.png "Resource groups")

3. On the Resource groups blade, select **Add** on the toolbar to create a new resource group.

    ![The Add button on the Resource groups toolbar is highlighted.](media/resource-groups-add.png "Add resource group")

4. On the **Create a resource group** Basics tab, enter the following:

    - **Subscription**: Select the subscription you are using for this exercise.
    - **Resource group**: Enter `udacity-exercises` or another name unique within your subscription.
    - **Region**: Select any available region, but preferably one close to your location. **Note**, you will use this same region for all other resources you create during this exercise.

    ![The values indicated above are entered into the create a resource group basics tab.](media/create-a-resource-group-basics.png "Create a resource group basics tab")

5. Select **Review + create** and on the Review + create tab, ensure the `validation passed` message is displayed and then select **Create**.

    ![The create a resource group review and create tab is displayed with the validation passed and create button highlighted.](media/create-resource-group-review-create.png "Review new resource group settings")

6. When the resource has been successfully created, select the notifications icon on the Azure header bar and then select **Go to resource group** in the **Resource group created** notification.

    ![The notifications icons is selected and highlighted on the Azure header bar and the Go to resource group button is highlighted under the Resource group created notification.](media/go-to-resource-group.png "Go to resource group notification")

## Task 2: Provision a Custom Vision service

In this task, you create a Custom Vision service in your Azure subscription.

1. On the **Resource group** blade, select **Add** on the toolbar.

    ![The Add button on the resource group toolbar is highlighted.](media/resource-group-add-resource.png "Add resource to resource group")

2. Enter `Custom Vision` into the search the marketplace box and press enter or select the result that appears below your typed text.

3. Select **Create** on the Custom Vision blade.

    ![The Create button is highlighted on the Custom Vision blade.](media/custom-vision-create.png "Create new Custom Vision service")

4. Configure a new **Custom Vision** by entering the follow settings:

    - **Create options**: Select **Both**. This will result in the creation of two `Cognitive Services` resources in your resource group; one for training and one for prediction.
    - **Subscription**: Select the subscription you are using for this exercise.
    - **Resource group**: Select the resource group you create previously.
    - **Name**: Enter a globally unique name, such as `udacitycustomvisionSUFFIX`, replacing `SUFFIX` with your initials or another string to make the name unique.
    - **Training location**: Select the same location you choose for your resource group above.
    - **Training pricing tier**: Select **Free F0**.
    - **Prediction location**: Select the same location you choose for your resource group above.
    - **Prediction pricing tier**: Select **Free F0**.

    >**Note**: You can only have one **F0** Custom Vision service provisioned in your subscription, so if you already have one, select **Standard S0** for both the training and prediction locations above.

    ![The Custom Vision basics tab is populated with the values specified above.](media/create-custom-vision-service-basics.png "Create Custom Vision service")

5. Select **Review + create** and, as you did previously, ensure the validation passed and then select **Create**.

6. When the deployment of the Custom Vision service completes, select **Go to resource** on the deployment blade. This will take you to the `training` Cognitive services resource.

    ![The Go to resource button is highlighted on the deployment screen.](media/custom-vision-deployment-complete.png "Deployment complete")

## Step 2: Train and deploy an image classification model

In this step, you will upload images to the Custom Vision service and use them to train an image classifier. You will then publish the trained model to your prediction Cognitive service for consumption.

### Task 1: Download images to train the classification model

In this task, you download some images of cats and dogs that can be used for training a multiclass classification model.

1. Download and extract the training images from the [Udacity AI Fundamentals GitHub repo](https://github.com/udacity/AI_fundamentals/blob/main/lesson-4/training-images/training-images.zip?raw=true).

    > **TODO**: Ensure GitHub repo for downloading training images is correct and publicly accessible for downloading files.

    >**Note**: The project will use classify images as containing either cats or dogs, so the training images are grouped into two folders, `cats` and `dogs`.

### Task 2: Train a Multiclass Classification model in Custom Vision

In this task, you upload and tag the `cat` and `dog` images you downloaded in the previous task and use those to train an image classification model.

1. From the open `training` Cognitive services blade in the Azure portal, select the **Quick start** menu item from the left-hand navigation menu and then select the **Custom Vision portal** link on the Quick start blade.

    ![The Quick start menu item is selected and highlighted in the left-hand menu and the Custom Vision portal link is highlighted on the Quick start blade.](media/custom-vision-portal-link.png "Custom Vision portal link")

2. Select **Sign In** and enter the credentials for the Azure portal, if prompted.

    ![The Sign In button is highlighted on the Custom Vision home page.](media/custom-vision-sign-in.png "Custom Vision")

3. In the Custom Vision portal, select **New Project**.

    ![The New Project tile from the Custom Vision portal is displayed with New Project highlighted.](media/custom-vision-new-project-tile.png "New Project")

4. In the Create new project dialog, enter the following:

    - **Name**: Enter `Pet Classification`.
    - **Description**: Enter a short description, such as `Image classifier for dogs and cats`.
    - **Resource**: Select your training Cognitive service.
    - **Project Types**: Choose `Classification`.
    - **Classification Types**: Choose `Multiclass`.
    - **Domains**: Choose `General`.

    ![On the Create new project dialog, the values specified above are entered into the form.](media/custom-vision-create-new-project.png "Create new Custom Vision project")

5. Select **Create project**.

6. In the Custom Vision project, select **Add images** and browse to the directory into which you extracted the training images you downloaded above. Select the **cats** folder, select all of the images in the folder, and select **Open**. Enter `cat` into the **My Tags** field and then select **Upload 15 files**.

    ![The cat images have been selected and the tag of "cat" has been entered into the My tags field.](media/upload-cat-images.png "Image upload")

7. Repeat step 6, this time selecting the **dogs** folder and entering `dog` into the **My Tags** field. There should be 15 dog images uploaded.

    ![The dog images have been selected and the tag of "dog" has been entered into the My tags field.](media/upload-dog-images.png "Image upload")

8. Select **Train** to select a training type.

    ![On the Custom Vision toolbar, the Train button is highlighted.](media/train-classification-model.png "Custom Vision toolbar")

9. Choose the `Quick training` training type and select **Train**.

    >**Note**: Training may take a few minutes to complete.

    ![On the Choose training type dialog, Quick training is selected and highlighted and the Train button is highlighted.](media/choose-training-type.png "Choose training type")

10. When the model training is complete, observe the results.

    > **Model performance statistics**
    >
    > **AP** provides a measure of the accuracy of a classification model by summarizing the precision and recall values.
    >
    > **Precision** indicates how likely your classification model is to be correct if it predicts a tag.
    >
    > **Recall** informs you of the percentage of image tags that should have been correctly predicted by your model that were actually tagged.

    ![The output of training iteration 1 are displayed.](media/training-iteration-1.png "Training Iteration 1 results")

11. Test your model selecting **Quick Test** on the toolbar.

    ![On the Custom Vision toolbar, the Quick Test button is highlighted.](media/toolbar-quick-test.png "Custom Vision toolbar")

12. Use the following image URLs for testing by copying and pasting each one into the **Image URL** box and selecting the box containing an arrow:

    - <https://github.com/udacity/AI_fundamentals/blob/main/lesson-4/testing-images/cat-test-001.jpg?raw=true>
    - <https://github.com/udacity/AI_fundamentals/blob/main/lesson-4/testing-images/dog-test-001.jpg?raw=true>

    ![In the Quick Test dialog, the URL containing image cat-test-001.jpg is entered into the Image URL and the Image URL and submit button are highlighted. The predication results are highlighted, showing a prediction that the image is a cat with a probability of 99.9%.](media/quick-test-cat.png "Quick Test")

13. Close the **Quick Test** dialog when you are done with each test, but keep the Custom Vision Pet Classification window open for the next task.

### Task 3: Deploy the custom image classification model

In this task, you will publish your classification model to the prediction Cognitive service, so it can be consumed by external resources.

1. Back in the Pet Classification project in Custom Vision studio, select **Publish** on the **Performance** tab of your model.

    ![The Publish button is highlighted on the Performance tab, which is also highlighted.](media/publish-button.png "Publish")

2. Name the model `pet-classifier`, select your **-Prediction** resource from the list, and then select **Publish**.

    > This will deploy your image classification model to the prediction cognitive services resource that was created when you provisioned the Custom Vision service.

    ![In the Publish Model dialog, pet-classifier is entered into the Model name field and the -Prediction resource is selected in the Prediction resource drop down list. The Publish button is highlighted.](media/publish-model.png "Publish Model")

3. Next, open your Custom Vision project's `Settings` page by selecting the gear icon on the toolbar and leave the page open for the next task. You will need the `Project Id` value to complete the steps contained within the notebook below.

    > **Important**: Do NOT copy the **Key** and **Endpoint** value from the project settings page for use in the notebook below. These point to the training cognitive service and will not provide access to your deployed classification model.

    ![The project settings icon is highlighted and on the settings page the Project Id field is highlighted.](media/project-settings.png "Project settings")

4. In a new browser window, return to the Azure portal and navigate back to your resource group. Within your resource group, select the **-Prediction** Cognitive service.

    ![The -Prediction resource is highlighted in the list of resources in the resource group.](media/resource-group.png "Resource group")

5. On the prediction cognitive service blade, select **Keys and Endpoints** from the left-hand menu and leave this page open. You will need the `Key` and `Endpoint` values from your prediction cognitive service resource.

    ![The Keys and Endpoints blade for the prediction cognitive service is displayed, with Keys and Endpoints highlighted in the left-hand menu and the Key 1 and Endpoint values highlighted.](media/prediction-keys-and-endpoints.png "Keys and Endpoints")

## Step 3: Create an image classification solution using a Jupyter notebook

In this step, you will create an Azure Machine Learning workspace that you an use to build an image classification solution using Python in a Jupyter notebook.

### Task 1: Create an Azure Machine Learning workspace

In this task, you create an Azure Machine Learning workspace to provide an environment capable of hosting and running a Jupyter notebook.

1. In a new browser window, open the Azure portal and return to your resource group.

2. On the **Resource group** blade, select **Add** on the toolbar.

    ![The Add button on the resource group toolbar is highlighted.](media/resource-group-add-resource.png "Add resource to resource group")

3. On the New blade, enter `Machine Learning` into the search the marketplace box, and press enter on your keyboard.

    ![Machine Learning is entered into the search the marketplace box and highlighted on the New blade.](media/new-machine-learning.png "New Machine Learning")

4. Select **Create** on the Machine Learning blade.

    ![The Create button is highlighted on the Machine Learning blade.](media/create-machine-learning.png "Create Machine Learning")

5. On the Create a machine learning workspace **Basics** tab, enter the following:

    - **Subscription**: Select the subscription you are using for this exercise.
    - **Resource group**: Select the resource group you created for this exercise.
    - **Workspace name**: Enter `udacity-ml-workspace`.
    - **Region**: Select the region you used for your resource group above.
    - **Storage account**: Accept the default assigned value to create a new storage account.
    - **Key vault**: Accept the default assigned value to create a new key vault.
    - **Application insights**: Accept the default assigned value to create a new Applications Insights instance.
    - **Container registry**: Accept the default assigned value of **None**.

    ![On the Create a machine learning workspace blade, the values indicated above are entered into the form.](media/create-machine-learning-workspace-basics.png "Create a machine learning workspace")

6. Select **Review + create**, ensure you see the validation passed message, and then select **Create**.

7. Once your AML workspace deployment completes, open the [Azure Machine Learning Studio](https://ml.azure.com/) in a new browser window.

    ![The home page of Azure Machine Learning studio is displayed.](media/aml-studio.png "Azure Machine Learning studio")

### Task 2: Create a compute instance

In this task, you create the virtual machine that will host your Jupyter environment for running your notebook.

1. On the home page on Azure Machine Learning studio, select **Create new** and then select **Compute instance** from the context menu.

    ![The Create new button is highlighted in Compute instance is highlighted in the context menu.](media/create-new-compute-instance.png "Create new")

2. On the **Create compute instance** Virtual machine page, select the following:

    - **Virtual machine type**: Choose **CPU**.
    - **Virtual machine size**: Choose the `Standard_DS3_v2` virtual machine.

    ![The virtual machine page of the create compute instance dialog is displayed with the selections indicated chosen and highlighted.](media/create-compute-instance-vm.png "Create compute instance")

3. Select **Next** on the Create compute instance dialog.

4. Enter `udacity-ml-vm` for the **Compute name** and then select **Create**.

    > **Note**: It takes a few minutes for the compute instance to start, so wait until it has completed.

    ![The name udacity-ml-vm is entered into the compute name field and highlighted. The Create button is highlighted.](media/create-compute-instance.png "Create compute instance")

### Task 3: Use the Jupyter environment to run an image classification solution

In this task, you will launch the Jupyter environment running on your AML compute instance and download a notebook that contains the code for an image classification solution.

1. Launch the `Jupyter` interface for your compute instance by selecting the `Jupyter` Application URI associated with it.

    ![The Jupyter link for the new compute instance is highlighted.](media/jupyter-link.png "Jupyter link")

2. In the Jupyter environment, select **New** and **Terminal** to open a terminal window.

    ![In the Jupyter environment, the New drop down is selected and highlighted and Terminal is highlighted in the context menu.](media/jupyter-new-terminal.png "New terminal")

3. At the prompt, clone the Udacity AI Fundamentals GitHub repo containing the notebook for this exercise by pasting and executing the following code:

    ```bash
    git clone https://github.com/udacity/AI_fundamentals.git
    ```

4. Close the terminal window and return to the Jupyter environment window and open the `Image-Classification.ipynb` notebook in the `AI_fundamentals/lesson-4` folder.

    > **Note**, you may need to hit refresh on the window to see the `AI_fundamentals` folder.

    ![In the Jupyter file system, the AI_fundamentals/lesson-4 folder is highlighted and the Image-Classification.ipynb notebook is highlighted.](media/jupyter-image-classification-notebook.png "Image classification notebook")

5. Follow the instructions within the notebook to complete the rest of the exercise.
