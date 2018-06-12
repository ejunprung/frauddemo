# SKIL Anomaly Detection Application

A description of this application can be found at https://blog.skymind.ai/p/5dac6e86-aa79-4104-befe-a32cc7ec3d10/.

## Files

This repository contains three files.

1. Fraud Autoencoder.json - An importable Zeppelin notebook containing Python code to train an Autoencoder. 
2. Fraud MLP.json - An importable Zeppelin notebook containing Python code to train a Multilayer Perceptron. 
3. skil_anomaly_detection_python_app.zip - Client API to query the deployed Multilayer Perceptron model in SKIL. 

## Client API Instructions 

skil_anomaly_detection_python_app.zip contains a client API to query the Multilayer Perceptron model in SKIL. 

1. Unzip skil_anomaly_detection_python_app.zip.
2. Run `mvn package` using the terminal within the client_app subdirectory to obtain the JAR file.
3. Type `java -jar skil-example-anomaly-detection-1.0.0.jar --feature fraud.csv --endpoint http://localhost:9008/endpoints/test/model/anomaly-detection/default/` to query the model and obtain a prediction (fraud or not).
