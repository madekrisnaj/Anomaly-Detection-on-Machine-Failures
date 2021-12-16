# Anomaly Detection on Machine Failures

## Overview
Condition Based Maintenance (CBM) uses sensor to to collect real-time measurement (ie. pressure, temperature, and vibration). CBM data allows maintenance personnel to perform maintenance at the exact moment it is needed, prior to failure. 

Key take-aways from use case:
* How to build an anomaly detection model using [**Long Short-Term Memory (LSTM)**](https://www.tensorflow.org/api_docs/python/tf/keras/layers/LSTM.html) Autoencoder Model.

## Data Description
We will use vibration sensor readings from NASA Acoustics and Vibration Database. sensor readings were taken on four bearings that were run to failure under constant load and running conditions. The vibration measurement signals are provided for the datasets over the lifetime of the bearings until failure. Failure occurred after 100 million cycles with a crack in the outer race.

You can download the sensor data [here](https://github.com/madekrisnaj/Anomaly-Detection-on-Machine-Failures/tree/main/data).

## Anomaly Detection
Anomaly detection is the process of finding outliers in a given dataset. Outliers are the data objects that stand out amongst other objects in the dataset and do not conform to the normal behavior in a dataset. Anomaly detection is a data science application that combines multiple data science tasks like classification, regression, and clustering (Kotu & Deshpande, 2019).

The assumption is that normal behavior is the quantity of "normal" data available, whereas anomalies are exceptions to the normal state up to the point where normal modeling is performed.

## Data Exploration
##### All Data Visualization
Based on the overall data plot. We can see the period of normal data and anomalous data. This is necessary in dividing the dataset into training and testing. We define the train and test datasets based on operating conditions, from the vizualization we can see data which represent normal operating condition are until around February 15th, 2004.

<a href="https://ibb.co/x1tTZ8V"><img src="https://i.ibb.co/48nrkgB/1.png" alt="1" border="0"></a>

#### **Training Data**
We plot the training data which represent normal operating conditions.

<a href="https://ibb.co/68dGQFh"><img src="https://i.ibb.co/VxKb6Ty/2.png" alt="2" border="0"></a>

#### **Testing Data**
Next, we can see the test dataset sensor readings over time

<a href="https://ibb.co/wRpLJZR"><img src="https://i.ibb.co/t4YhZw4/3.png" alt="3" border="0"></a>

We can see that near the failure point, the bearing vibration become oscillate. 

#### **Frequency Perspective**
To view the vibrations in a frequency perspective, the data is transformed using the [**Fourier transform**](https://www.dataq.com/data-acquisition/general-education-tutorials/fft-fast-fourier-transform-waveform-analysis.html#:~:text=Simply%20stated%2C%20the%20Fourier%20transform,magnitude%2C%20frequency%2C%20and%20phase).

<a href="https://ibb.co/tQRcF56"><img src="https://i.ibb.co/VJ6D58G/5.png" alt="5" border="0"></a>

There is nothing notable about the normal operation data.

<a href="https://ibb.co/Gdk7d9P"><img src="https://i.ibb.co/7SVvSQy/4.png" alt="4" border="0"></a>

We can see the increase in the frequency amplitude and energy in the system leading up to the bearing failures.

## Model Building
Long Short-Term Memory (LSTM) are a type of recurrent neural network capable of learning order dependence in sequence prediction problems. (Browniee, 2017). This is a behavior required in complex problem domains like machine translation, speech recognition, and more. LSTMs are a complex area of deep learning. It can be hard to get your hands around what LSTMs are, and how terms like bidirectional and sequence-to-sequence relate to the field.

For our model we will use an autoencoder neural network architecture. This architecture was chosen to handle model weaknesses due to the selection of training data from normal conditions.

<a href="https://ibb.co/wrG9JhB"><img src="https://i.ibb.co/R4rxhTY/6.png" alt="6" border="0"></a>

For 100 epochs and batxh size is 10, we fit the model to training data. We can plot the training losses to evaluate our model's performance.

<a href="https://ibb.co/Bfcx2sQ"><img src="https://i.ibb.co/wdBXh6P/7.png" alt="7" border="0"></a>

#### **Loss Distribution**
By plotting the distribution of the calculated loss in the training set, we can determine a suitable threshold value for identifying an anomaly. In doing this, one can make sure that this threshold is set above the noise level so that false positives are not triggered.

<a href="https://ibb.co/9npdN8c"><img src="https://i.ibb.co/wyd2R0B/8.png" alt="8" border="0"></a>

Based on the histogram, we get treshold value of around 0.2625

#### **Result Failure Time Plot**
We visualize the result over time. The red line indicates our treshold value of 0.2625.

<a href="https://ibb.co/NZzYXhw"><img src="https://i.ibb.co/6g5s2h6/9.png" alt="9" border="0"></a>

## Conclusion
By analyzing past trends of healthy, the model learns the expected trend with acceptable variance (hyperparameter). From the above vizualization, we see that the model is able to detect the anomaly approximately 3 days ahead of the actual bearing failure.

## References
https://machinelearningmastery.com/gentle-introduction-long-short-term-memory-networks-experts/ https://www.sciencedirect.com/science/article/pii/B9780128147610000137
