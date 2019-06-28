# Sentiment Analysis

The notebook and Python files provided here, result in a simple web app which interacts with a deployed recurrent neural network performing sentiment analysis on IMBD movie reviews. This project assumes some familiarity with SageMaker.

## Getting Started

### General Outline

Recall the general outline for SageMaker projects using a notebook instance.

Download or otherwise retrieve the data.
Process / Prepare the data.
Upload the processed data to S3.
Train a chosen model.
Test the trained model (typically using a batch transform job).
Deploy the trained model.
Use the deployed model.

Deploy and use your trained model a second time. In the second iteration we will customize the way that your trained model is deployed by including some of our own code. In addition, our newly deployed model will be used in the sentiment analysis web app.

### Prerequisites

In this project you will be training a recurrent neural network which means that you will most likely want access to a GPU enabled instance for training. It should be possible to train your model without using a GPU instance, however, the length of time required to do so will likely be very long.

The smallest GPU instance available when using SageMaker is the ml.p2.xlarge instance and it is perfectly adequate for completing the project. Depending on the default region that was used during the creation of your AWS account the default number of ml.p2.xlarge instances allowed may be 0.

### Installing

### Use the model for the web app

### 1 - Setting up a Lambda function

The first thing we are going to do is set up a **Lambda function**. This Lambda function will be executed whenever our public API has data sent to it. When it is executed it will receive the data, perform any sort of processing that is required, send the data (the review) to the SageMaker endpoint we've created and then return the result.

**Part A**: Create an IAM Role for the Lambda function

Since we want the Lambda function to call a SageMaker endpoint, we need to make sure that it has permission to do so. To do this, we will construct a role that we can later give the Lambda function.

Using the AWS Console, navigate to the IAM page and click on Roles. Then, click on Create role. Make sure that the AWS service is the type of trusted entity selected and choose Lambda as the service that will use this role, then click Next: Permissions.

In the search box type sagemaker and select the check box next to the AmazonSageMakerFullAccess policy. Then, click on Next: Review.

Lastly, give this role a name. Make sure you use a name that you will remember later on, for example LambdaSageMakerRole. Then, click on Create role.

**Part B**: Create a Lambda function

Using the AWS Console, navigate to the AWS Lambda page and click on Create a function. When you get to the next page, make sure that Author from scratch is selected. Now, name your Lambda function, using a name that you will remember later on, for example sentiment_analysis_func. Make sure that the Python 3.6 runtime is selected and then choose the role that you created in the previous part. Then, click on Create Function.

On the next page you will see some information about the Lambda function you've just created. If you scroll down you should see an editor in which you can write the code that will be executed when your Lambda function is triggered.

### 2 - Setting up API Gateway

Now that our Lambda function is set up, it is time to create a new API using API Gateway that will trigger the Lambda function we have just created.

Using AWS Console, navigate to Amazon API Gateway and then click on Get started.

On the next page, make sure that New API is selected and give the new api a name, for example, sentiment_analysis_api. Then, click on Create API.


## Running the tests

Now we have created an API, however it doesn't currently do anything. What we want it to do is to trigger the Lambda function that we created earlier.

Select the Actions dropdown menu and click Create Method. A new blank method will be created, select its dropdown menu and select POST, then click on the check mark beside it.

For the integration point, make sure that Lambda Function is selected and click on the Use Lambda Proxy integration. This option makes sure that the data that is sent to the API is then sent directly to the Lambda function with no processing. It also means that the return value must be a proper response object as it will also not be processed by API Gateway.

Type the name of the Lambda function you created earlier into the Lambda Function text entry box and then click on Save. Click on OK in the pop-up box that then appears, giving permission to API Gateway to invoke the Lambda function you created.

### Break down into end to end tests

The last step in creating the API Gateway is to select the Actions dropdown and click on Deploy API. We will need to create a new Deployment stage and name it anything you like, for example prod.

You have now successfully set up a public API to access our SageMaker model. Make sure to copy or write down the URL provided to invoke our newly created public API as this will be needed in the next step. This URL can be found at the top of the page, highlighted in blue next to the text Invoke URL.

## Deployment

After that we have a publicly available API, we can start using it in a web app. For our purposes, we should provide a html file which can make use of the public api we created earlier.

In the repository folder there should be a file called index.html. Download the file to your computer and open that file up in a text editor of your choice. There should be a line which contains **REPLACE WITH PUBLIC API URL**. Replace this string with the url that you wrote down in the last step and then save the file.

Now, if we open index.html on local computer, our browser will behave as a local web server and we can use the provided site to interact with our SageMaker model.

## Built With

* [Amazon SageMaker](https://aws.amazon.com/sagemaker/) - The web framework used
* [Amazon S3](https://aws.amazon.com/s3/) - The web storage used
* [Amazon API](https://aws.amazon.com/api-gateway/) - The API used

## Authors

* **Keyvan Tajbakhsh** - [keyvantaj](https://github.com/keyvantaj)

See also the list of [contributors](https://github.com/udacity/machine-learning/graphs/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
