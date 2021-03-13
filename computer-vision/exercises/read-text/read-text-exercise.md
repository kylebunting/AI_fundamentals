# Exercise: Read Text With Computer Vision Service

## Indroduction

Short description of the OCR APIs capabilities contained within the Computer Vision service.

## Instructions

You will complete this exercise using your Azure subscription. If you don't have one, you can sign up for a free trial at <https://azure.microsoft.com/free>.

You will not be using a Udacity workspace to complete this exercise.

> **Note**: All the Azure resource used for this exercise should be created in the same region to minimize egress charges and network latency.

## Task list

1. Open a web browser, navigate to the [Azure portal](https://portal.azure.com/), and sign in using the account associated with your Azure subscription.

2. In the Azure portal, create a new **Resource group** named `udacity-exercises`, or something similar, to host the resources you will be creating for this exercise.

3. Create a new **Computer Vision** service using the `Free F0` pricing tier.

    >**Note**: You can only have one **F0** Computer Vision service provisioned in your subscription, so if you already have one, select **Standard S0** for the pricing tier.

4. In the Azure portal, navigate to the `Keys and Endpoints` page for you new Computer Vision service and leave the page open for the next task. You will need to the `Key` and `Endpoint` values to complete the steps contained within the notebook below.

5. Return to the Azure portal and create a new **Azure Machine Learning workspace** named `udacity-ml-workspace` in your resource group, if it does not already exist from a previous exercise.

6. Open [Azure Machine Learning Studio](https://ml.azure.com/) and then create a new **Compute instance** named `udacity-ml-vm` using the `Standard_DS3_v2` virtual machine, if one does not already exist from a previous exercise.

> **Note**: It takes a few minutes for the compute instance to start, so wait until it has completed.

1. Launch the `Jupyter` interface for your compute instance by selecting the `Jupyter` Application URI associated with it. In the Jupyter environment, select **New** and **Terminal** to open a terminal window and at the prompt clone the GitHub repo containing the notebook for this exercise by pasting and executing the following code:

    ```bash
    git clone https://github.com/kylebunting/udacity-ai-fundamentals.git
    ```

    > **TODO**: Update git clone url to appropriate GitHub repo.

2. Return to the Jupyter environment window and open the `Lesson-3-Read-Text.ipynb` notebook in the `udacity-ai-fundamentals/Lesson-3-Computer-Vision` folder and follow the instructions within the notebook to complete the rest of the exercise. Note, you may need to hit refresh on the window to see the `udacity-ai-fundamentals` folder.
