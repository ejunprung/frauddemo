# SKIL Anomaly Detection Application

The full tutorial can be found at https://blog.skymind.ai/p/5dac6e86-aa79-4104-befe-a32cc7ec3d10/.

## Files

This repository contains three files.

1. *Fraud Autoencoder.json* - An importable Zeppelin notebook containing Python code to train an Autoencoder.
2. *Fraud MLP.json* - An importable Zeppelin notebook containing Python code to train a Multilayer Perceptron (MLP).
3. *skil_anomaly_detection_python_app.zip* - Client API to query the deployed Multilayer Perceptron model.

## Client API Instructions

*skil_anomaly_detection_python_app.zip* contains a client API, written in Java, which retrieves predictions from the MLP deployed in SKIL.

1. Run `mvn package` using the terminal within the client_app subdirectory to obtain the JAR file.
2. Type `java -jar skil-example-anomaly-detection-1.0.0.jar --feature fraud.csv --endpoint http://localhost:9008/endpoints/test/model/anomaly-detection/default/` to query the model and obtain a prediction (fraud or not fraud). Remember to replace "localhost" with the correct host if necessary.

## Training Dataset

We use the [PaySim dataset](https://www.kaggle.com/ntnu-testimon/paysim1/data). PaySim is a synthetically created dataset of over 1,000,000 mobile money transaction. To reduce the time it takes to train our models, we pluck a randomized subsample of around 10% or 100,000 examples from the full PaySim dataset.

## Data Cleansing

In order to feed our machine learning models, we need to transform the raw CSV data into usable vector formats. The features of the PaySim dataset contains both categorical and numerical values which must be converted into floats.

*step, isFlaggedFraud* are integers which must be converted into floats.
*type, nameOrig, nameDest* must be converted from characters into categorical values. From there, we convert the categorical values into floats as well.

The remaining columns are already in the proper type (floats) so there is nothing else we need to do. Now that our data is properly transformed, we scale all values between 0 and 1 to suppress the impact of outliers.

## Methodology

### Multilayer Perceptron (MLP)

A Multilinear perceptron is a supervised deep learning model intended to perform binary classification such as fraud or not fraud. Because we have a relatively large labeled dataset, we can teach a MLP to learn inherent differences between a *known* fraudulent and a *known* normal transaction.

To do this, we define the model architecture and feed our labeled training dataset (X_train, y_train) into the MLP. Using the labels (fraud or not fraud), the MLP should be able to differentiate unique patterns of a fraudulent transaction and unique patterns of a normal transaction.

A supervised approach tends to perform very well on well-established and known items of interest.

### Autoencoder

An autoencoder is an unsupervised deep learning model intended to learn structure in the data. The idea is to train a model to learn what a normal transaction should look like and compare the learned representation to a fraudulent transaction using reconstruction error. The hypothesis is that a fraudulent transaction will look very anomalous (and thus, have high reconstruction error) to a normal transaction (which will have very low or zero reconstruction error).

To achieve this, we simply take all normal (or not fraudulent) transactions and feed only those items into our autoencoder. In this way, we can teach the autoencoder what a normal transaction should look like and use that as a the baseline comparison.

An unsupervised approach tends to perform much worse, but it is very good at catching novel items (unknown unknowns) which are near impossible to proactively detect.
