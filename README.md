# Quantized Machine Learning Classifier #

**This Project is [Currently Hosted on BitBucket](https://bitbucket.org/joexdobs/ml-classifier-gesture-recognition)**  

The Quantized Classifier is a high performance,  high precision classifier built using knowledge I gained while working on classifiers to predict stock price movement over a period of several years.   For some data sets it delivers results equal or better than Deep Learning provided by Tensorflow while running faster and with fewer dependencies.

## How It works:

The Quantized classifier uses some features from KNN,  Bayesian probability, Clustering and Ensemble techniques to build an in memory training set that is much smaller than the input source data.  It is ideal for very large data sets that exceed RAM.     

I leverages a important principal I discovered in stock data which is that similarity on a given feature tends to be measured by numbers that are close together.   For example, if measuring the percentage a stock has risen in the last day.    Those that have risen by 1% to 1.1% are more similar than those that have risen by 2%.   This principal allows values to be clustered in evenly sized groups with classification statistics measured at the group level without retaining the original training data.   This seems simple but it can deliver blinding fast training,  extremely fast classification and seems to deliver very accurate results for non-image classification tasks. 

> ####How well does it work:####
> In each of these cases except Liver Disorder the Quantized classifier produced higher precision when forced to 100% recall than the a deep learning a Deep learning CNN trained with n_epoch = 30.  The Quantized classifier also ran faster with less RAM.  
> * Predict Breast Cancer 96%
> * Classify wine subjective taste 99%
> * Classify probable death or survival of titanic passengers 81% 
> * Predict Diabetes 69.41% 
> * Predict liver disorder 62.5%
>
> Every engine has domains where they will excel.  The Quantized classifier is designed for applications where the meaning of a feature remains consistent for all samples.   EG: If feature 1 is measuring the size of mole in mm then feature 1 should always measure a mole in mm.     
> CNN are superior for image classification and image classification is not a problem I plan to tackle with Quantized classifier. 

### Easy to get up and running

> * Install GO 
> * Add GO to the PATH
> * Run one scrip makeGO to build the EXE
> * Now you can start running the example cases using the included data.
>
> After spending days working out the Tensoflow, python,  scikit, numPy, tlearn dependency chains to get the demonstration programs  to run on windows 10.  I felt that something making the Quantized classifier easy to build and run was super important.  

## Data and Pattern Discovery 
One area where the Quantized classifier excels is using the optimizer to discover important data elements.   For example:
* It can discover that when predicting breast cancer skin thickness is far less important than uniform Cell size.     
* It can discover that grouping age into 3 buckets provides better classification looking at only two or creating 5 groups.  
* It could discover that age produces a negative value reducing prediction accuracy.  

This kind of discovery feedback can help data scientists discover what features are important in their data and how the patterns combine to enable better prediction.  The cancer doctors in the breast cancer example chose to classify each measurement as an integer between 0 and 10 and it worked well.  The Quantized engine could have accepted a simple measurement and deduced that 8 buckets may have worked better. 

At it's extreme you could imagine dumping hundreds of features worth of data for predicting which advertisments a given user buy from into the system and let it tell you which of those features are actually useful when making that prediction.   This use of the engine may turn out to be even more important than the classification capability.      


## Great Samples Included 
One hassle when using any new ML engine is the amount of work and coding with unfamiliar API required to test with your data idea.  

The Quantized classifier automatically builds the ClassifyFiles executable that can be ran from the command line on new data.  If you can create two new CSV files one for training and one for testing, then you can test your idea.   You can use the same utility to classify new data saving the results in a CSV. 

The data for a nice set of initial tests is included in the data directly properly formatted to use with the engine.     There are also a series of scripts that will run the test for each one of those data sets.    

There is more functionality available if you are willing to write some code and learn the library but you could get started and go quite a ways on the command line.


## HTTP Interface 
Moving from trivial tests to production is always a challenge with machine learning libraries.  Training the engine always consumes time so trained ML engines need to stay loaded in RAM ready to run if there will be much load. This means using a file based CSV Input -> CSV output that works well in testing will not work well in production.  

A surprising amount of pluming code can be required to integrate the machine learning system into the production applications.

To simplify this the Quantized Classifier provides a server component where training data, classification request and data exploration can be managed via a REST/JSON interface.  One reason we chose GO as the implementation language is that GO makes it relatively easy provide a long lived production quality HTTP server ready to integrate with other SOA capable software.  

## Tensorflow Examples
To ensure we have proper comparisons of the classification results I have written parallel versions in Python that use Tensorflow.   These examples read the same data files and produce similar output so it is easy to compare the results and time consumed.   These are in the tlearn directory.   

**This Project is [Currently Hosted on BitBucket](https://bitbucket.org/joexdobs/ml-classifier-gesture-recognition)**  