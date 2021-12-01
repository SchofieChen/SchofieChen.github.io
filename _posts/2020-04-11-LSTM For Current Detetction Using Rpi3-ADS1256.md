---
layout: post

#event information
title:  "Real-Time Current Anmoly Detection in DC Motor"
cover: ![GITHUB]( https://raw.githubusercontent.com/SchofieChen/SchofieChen.github.io/master/_picture/STM32F4Discovery.png "She is my daughter")
date:   2020-04-11
start_time: "09:00"
end_time: "12:00"

#event organiser details
organiser: "Schofie Chen"
organiser_email: "weicc80720@gmail.com"
organiser_name : "Schofie Chen"



---
# 1. ADC RNN Predicition
This side project is based on [ADS1256 Package](https://github.com/SchofieChen/High-Speed-ADS1256)
you can adjust parameter of initialize e.g. SPS, PGA etc.. this scenario is detect general motor as servo motor,
according to Nyquist Sampling frequency theorem. we need 2.65 ↑ sampling rate (2.65 * 60 = 159), that we can adjust sampling rate more than 159 setting as below, 
we can choose DRATE_500 or DRATE_1000 more than 159, remember when modify file you must recompile binary to be your RPI Binary library, BTW why I don't write firmware by python code
python code is interpreter it can't not handle real-time data even if using Linus OS. if you all done setting follow 

	DRATE_30000 = 0xF0, 
	DRATE_15000 = 0xE0,
	DRATE_7500  = 0xD0,
	DRATE_3750  = 0xC0,
	DRATE_2000  = 0xB0,
	DRATE_1000  = 0xA1,
	DRATE_500   = 0x92,
	DRATE_100   = 0x82,
	DRATE_60    = 0x72,
	DRATE_50    = 0x63,
	DRATE_30    = 0x53,
	DRATE_25    = 0x43,
	DRATE_15    = 0x33,
	DRATE_10    = 0x20,
	DRATE_5     = 0x13,
	DRATE_2d5   = 0x03

# 2. LSTM Neural Network for Time Series Prediction
LSTM built using the Keras Python package to predict time series steps and sequences. Includes sine wave and stock market data.

# 3. Requirements

Install requirements.txt file to make sure correct versions of libraries are being used.

[ADS1256 Package](https://github.com/SchofieChen/High-Speed-ADS1256)
* Python 3.5.x
* TensorFlow 1.11.0
* Numpy 1.15.0
* Keras 2.2.4
* Matplotlib 2.0.0
* Pandas 0.23.4
* Json 2.0.9
* Scipy 1.1.0



# 4. Result
ADC for sine wave:

![image](https://raw.githubusercontent.com/SchofieChen/SchofieChen.github.io/master/_picture/adc_collect_raw_data.png)

Connection As bellow : more information in [ADS1256 Package](https://github.com/SchofieChen/High-Speed-ADS1256)
![image](https://raw.githubusercontent.com/SchofieChen/SchofieChen.github.io/master/_picture/ADS1256-Rpi_Connection.png)


LSTM for sine wave sequential prediction:
![image](https://raw.githubusercontent.com/SchofieChen/SchofieChen.github.io/master/_picture/LSTM_prediction.png)

# 5. How to training model 
1. Get Data
in line31~33 you can set parameter and get ADS1256 data in ADC_SaveData.py, 
you should get more and more data to fit you working current model.(500 cycle) up
![image](https://raw.githubusercontent.com/SchofieChen/SchofieChen.github.io/master/_picture/Rpi-LSTM-GetData.png)
2. Json Config 
Setting including neurons and drop out layer and run run.py get new model in saved_models
![image](https://raw.githubusercontent.com/SchofieChen/SchofieChen.github.io/master/_picture/Rpi-LSTM-Training.png)
# 6 Test your Result 
Run ADC_Inference.py it will show each batch data prediction, if you wanna get error of between golden and failure 
you can Subtract point by point between golden and failure to confirm match percent 