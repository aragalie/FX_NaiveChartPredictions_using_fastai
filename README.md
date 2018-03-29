# FX price prediction using state-of-the-art image recognition Machine Learning algorithms
Experiment to see if an accurate prediction of long/short positions in FX can be done using state-of-the-art image recognition algorithms (via fast.ai library).

### How does it work

- Get the data you need in a pandas DataFrame
- Manipulate the data according to your needs
- Plot the data using matplotlib
- Save the plots as pictures with appropriate labels and placed in the appropriate data folder for later use
- Run the prediction model
- Be dissapointed with the prediction accuracy and try again :)

### 1. Oanda_Data_Retrieval

This is the initial step of data preparation, plotting and exporting as images. 
Note that even though i'm using this example for FX data (using [Oanda](https://www.oanda.com>) as a broker), with minimal code adjustment you can use your own data sources/DataFrames

##### Data retrieval and preparation

- Data is being pulled via Oanda's API for whatever time window you require. `Start` (e.g 2018-01-01) and `End` dates can be specified, `instrument` (e.g GBP_USD) as well as candle `freqency` (e.d M1 meaning 1 minute candles).
- You can find 2 files in the repo to help run an initial example, in case you don't have/don't want to make a Oanda account: 
```sh
`GBP_USD_M1_2018-03-01_2018-03-27.h5s` can be used in the `data/ViewPorts/valid/` folder (recent prices)
`GBP_USD_M1_2017-10-01_2018-02-28.h5s` can be used in the `data/ViewPorts/train/` folder
```
- In case you want to use this data, skip sections *4-6* in the Jupyter Notebook and load the .h5s files directly in the DataFrame at section *7*

- Data is then added to a pandas DataFrame and modeled accordingly to needs. In my case i add 2 trend indicators (Moving Average 50 and Bollinger Bands 20sma)

##### Data plotting

The fastai algorithm (from [Lesson 1](http://course.fast.ai/lessons/lesson1.html)) uses images labeled as`category.order_number.png`, and it expects to find them in the folder structure data/test/category and data/valid/category

As such, the following operations are being done using the prepared data:

- Plotting the price line
- Plotting the MA50 indicator on top
- Plotting the BollingerBands indicator on top
- Removing all axes and labels

##### Images export

Based on a specified trading rule, each plotted chart is saved as .png in it's respective folder and with the respective label (e.g buy, sell or hold). Each .png is saved as a square 250px image, which helps later on in the speed of the prediction model.

Note: the `Oanda_Data_Retrieval.ipynb` Jupyter NB needs to be run once for the `train` data generation and another time for the `valid` folder, making sure the code is changed accordingly (in sections *7* and *12*).

### 2. fastai_Prediction

This is the last step, running the model and checking the prediction accuracy.

#### Running the fastai model

Assuming that your images have been exported appropriately and that fastai library is in the same folder, run the Jupyter Notebook to check the accuracy of prediction


## Install

1. Clone this repo:
```sh
git clone https://github.com/aragalie/FX_NaiveChartPredictions_using_fastai.git
```
2. Install the fastai library in the same folder: [instructions here](https://github.com/fastai/fastai)

3. Install `oandapy`: [instructions here](https://github.com/oanda/oandapy)

4. Make sure you have the same `data` folder structure, or ensure to adjust the code in the Jupyter NBs to reflect your own structure:
```sh
data/ViewPorts/
               train/
                    /buy
                    /sell
                    /hold
               valid/
                    /buy
                    /sell
                    /hold            
```

## Run

Run the Jupyter Notebooks, test and ajust.

