# Anomaly Detection on Machine Failures

## Overview
Condition Based Maintenance (CBM) uses sensor to to collect real-time measurement (ie. pressure, temperature, and vibration). CBM data allows maintenance personnel to perform maintenance at the exact moment it is needed, prior to failure. 

Key take-aways from use case:
* How to build an anomaly detection model using [**Long Short-Term Memory (LSTM)**](https://www.tensorflow.org/api_docs/python/tf/keras/layers/LSTM.html) Autoencoder Model.

## Data Description
We will use vibration sensor readings from NASA Acoustics and Vibration Database. sensor readings were taken on four bearings that were run to failure under constant load and running conditions. The vibration measurement signals are provided for the datasets over the lifetime of the bearings until failure. Failure occurred after 100 million cycles with a crack in the outer race.

You can download the sensor data [here](https://github.com/madekrisnaj/Anomaly-Detection-on-Machine-Failures/tree/main/data)

<a href="https://ibb.co/x1tTZ8V"><img src="https://i.ibb.co/48nrkgB/1.png" alt="1" border="0"></a>
