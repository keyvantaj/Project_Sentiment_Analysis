# Project_Sentiment_Analysis

This project relate to building a plagiarism detector that examines a text file and performs binary classification; labeling that file as either *plagiarized* or *not*, depending on how similar that text file is to a provided source text. Detecting plagiarism is an active area of research; the task is non-trivial and the differences between paraphrased answers and original work are often not so obvious..

## Getting Started

### General Outline

This project will be broken down into the following main parts:

* Download or otherwise retrieve the data.
* Process / Prepare the data.
* Upload the processed data to S3.
* Train a chosen model.
* Test the trained model (typically using a batch transform job).
* Deploy the trained model.
* Use the deployed model.

### Prerequisites

* [NumPy](https://www.numpy.org/) - A fundamental package for scientific computing with Python.
* [Pandas](https://pandas.pydata.org/) - A library providing high-performance, easy-to-use data structures and data analysis tools.
* [ScikitLearn](https://scikit-learn.org/stable/index.html) - Simple and efficient tools for data mining and data analysis
* [Matplotlib](https://matplotlib.org/) - Matplotlib is a Python 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms
* [Pickle](https://docs.python.org/3/library/pickle.html) - The pickle module implements binary protocols for serializing and de-serializing a Python object structure.
* [Sea Born](https://seaborn.pydata.org/) - Seaborn is a Python data visualization library based on matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics.
* [boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) - Boto is the Amazon Web Services (AWS) SDK for Python. It enables Python developers to create, configure, and manage AWS services, such as EC2 and S3. Boto provides an easy to use, object-oriented API, as well as low-level access to AWS services.
* [SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-mkt-create-model-package.html) - SageMaker Python SDK is an open source library for training and deploying machine learning models on Amazon SageMaker.

You will also need to have software installed to run and execute a [Jupyter Notebook](http://ipython.org/notebook.html)

If you do not have Python installed yet, it is highly recommended that you install the [Anaconda](http://continuum.io/downloads) distribution of Python, which already has the above packages and more included. 

### Code

The project is divided into two parts. The code is provided in the `1_Data_Exploration.ipynb`,`SageMaker Project.ipynb` notebook file. You will also be required to use aws SageMaker platform in the section `Linear Learner` to execute the code. This section is executed on Amazon SageMaker platform notebook. LinearLearner is a buitlin algorithm and we are only able to train and deploy this algorithm on Amazon SageMaker.

### Run

In a terminal or command window, navigate to the top-level project directory `Project_Sentiment_Analysis/` (that contains this README) and run one of the following commands:

```bash
ipython notebook SageMaker Project.ipynb
```  
or
```bash
jupyter notebook SageMaker Project.ipynb.ipynb
```

This will open the Jupyter Notebook software and project file in your browser.

### Data

In this project datasets are provided by [Udacity](https://eu.udacity.com/) and limited to this project.

## Running the tests

Once our model is deployed, we can see how it performs when applied to the test data.
Assuming data is stored locally in data_dir and named test.csv. The labels and features are extracted from the .csv file.

We use our deployed `predictor` to generate predicted, class labels for the test data. Then we Compare those to the *true* labels, `test_y`, and calculate the accuracy as a value between 0 and 1.0 that indicates the fraction of test data that our model classified.

### Break down into end to end tests

In this project we choosed two models LinearLearner which is a builtin sagemaker algorithm and PyTorch Neural Network Classifier. After that we compare and select the best one.

To implement a custom classifier, we'll need to complete a `train.py` script. we've been given folder `serve` which hold starting code for  PyTorch model, respectively. This directory has a `train.py` training script.

## Built With

* [Amazon SageMaker](https://aws.amazon.com/sagemaker/) - The web framework used
* [Amazon S3](https://aws.amazon.com/s3/) - The web storage used
* [Amazon API](https://aws.amazon.com/api-gateway/) - The API used

## Authors

* **Keyvan Tajbakhsh** - [keyvantaj](https://github.com/keyvantaj)

See also the list of [contributors](https://github.com/udacity/machine-learning/graphs/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
