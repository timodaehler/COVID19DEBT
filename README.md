# Project: COVID-19 and EM Debt

## Brief description
This project looks at COVID-19 policies of emerging markets and their influence on sovereign bond spreads. 


## Contributors & contact information
* Prof. Joshua Aizenman (aizenman@usc.edu or josh.aizenman@gmail.com) 
* Prof. Yothin Jinjarak (yothin.jinjarak@vuw.ac.nz or yothin.jinjarak@gmail.com) 
* Timo Daehler (daehler@usc.edu or timo.daehler@gmail.com) 

The note taker and corresponding author for coding related questions is Timo Daehler. For general questions on the goal of the project, contact Joshua Aizenman or Yothin Jinjarak. 

## Structure of folder
Note: This folder is a also available as a GitHub respository ([link](https://github.com/timodaehler/COVID19DEBT.git)). The folder structure contains the following elements: 

* Code (for all scripts)
* Data (for both raw and edited data)
* Plots (for output figures of scripts)
* Output (for final data files and tables)


This project/repository contains all the R Scripts, data, and output and is work in progress. While sometimes time-intensive to read, the R scripts in this project are annotated in detail to alleviate minor amnesias and to make the code ready for collaboration and external review.

The constituent parts should be self-explanatory due to the careful naming. As an additional help, the documentation below acts as a log book to keep track of the different research steps taken. It also acts as a sticker note to record common decisions of the contributors. 

## Documentation

### First step: defining which countries are examined
In a first step, we had to choose which emerging markets we want to investigate. We made 
the constituents of the JPMorgan EMBI the main observations. I looked up which markets
the EMBI comprosies. It appears that there's 31 countries in the index. 
https://www.ishares.com/us/products/239572/ishares-jp-morgan-usd-emerging-markets-bond-etf
This data was obtained on Saturday 25 April 2020. 

I saw that some potentially interesting and important markets were not in the EMBI, for example
India and Thailand, which is why I am adding those to the sample. (See code below).

In addition, we originally talked about only including emerging markets with a Debt/GDP ratio above 
a threshold of 10% or 20%. To find out which ones those are, I first downloaded the Debt/GDP ratio of all avaiable countries from the IMF's global debt database. 
https://www.imf.org/external/datamapper/CG_DEBT_GDP@GDD/FADGDWORLD
I chose the indicator "Central Government Debt" for e.o.y. 2018 as 2019 was not comprehensive. 
I saved the data to IMF.xls
Next, I checked which countries the IMF classifies as Emerging Markets as per October 2019. 
https://www.imf.org/~/media/Files/Publications/WEO/2019/October/English/text.ashx?la=en
p. 166 - 167 contains the list of countries classified as EM by the IMF. 
I hand-coded the EM classified countries as 1 in the IMF.xls sheet. All other countries are coded 0.

### Second step: defining which countries are examined
### 



