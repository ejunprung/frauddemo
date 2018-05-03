{\rtf1\ansi\ansicpg1252\cocoartf1561\cocoasubrtf200
{\fonttbl\f0\fswiss\fcharset0 Helvetica;\f1\fnil\fcharset0 HelveticaNeue;}
{\colortbl;\red255\green255\blue255;\red53\green53\blue53;}
{\*\expandedcolortbl;;\cssrgb\c27059\c27059\c27059;}
\margl1440\margr1440\vieww13860\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 skil_anomaly_detection_python_app\
	contains the model server example\
	run mvn package using the terminal in client_app subdirectory to obtain JAR file\
	command for sending example to model server\
	
\f1 \cf2 java -jar skil-example-anomaly-detection-1.0.0.jar --feature fraud.csv --endpoint http://localhost:9008/endpoints/test/model/anomaly-detection/default/
\f0 \cf0 \
\
CSV files:\
fraud_actual.csv: scaled data values\
\
fraud_reconstructions.csv: reconstructed values using fraud_actual.csv with an autoencoder\
	internal test\
		MSE loss for fraud examples: 0.00115\
		MSE oss for legitimate examples: 0.000244\
\
JSON files:\
	Anomaly Detection Autoencoder.json: Zeppelin notebook for creating and training auto encoder\
	Anomaly Detection MLP.json: Zeppelin notebook for creating and training MLP network and adding model to experiment\
}