# Project: COVID-19 and EM Debt

## Contributors 
* Prof. Joshua Aizenman (aizenman@usc.edu) 
* Prof. Yothin Jinjarak (yothin.jinjarak@vuw.ac.nz) 
* Timo Daehler (daehler@usc.edu) 

## GitHub respository
Here's the [link](https://github.com/timodaehler/COVID19DEBT.git) to the GitHub repository. 

## Read me
This project/repository contains all the R Scripts, data, and output and is work in progress. While sometimes time-intensive to read, the R scripts in this project are annotated in detail to alleviate minor amnesias and to make the code ready for collaboration and external review.

The constituent parts should be self-explanatory due to the careful naming. As an additional help, the documentation below acts as a log book to keep track of the different research steps taken. It also acts as a sticker note to record common decisions of the contributors. 

## Documentation
In a first step, we had to choose which emerging markets we want to investigate. We made 
the constituents of the JPMorgan EMBI the main observations. I looked up which markets
the EMBI comprosies. It appears that there's 31 countries in the index. 
https://www.ishares.com/us/products/239572/ishares-jp-morgan-usd-emerging-markets-bond-etf
This data was obtained on Saturday 25 April 2020. 

I saw that some potentially interesting and important markets were not in the EMBI, for example
India, Thailand and South Korea, which is why I am adding those to the sample. (See code below).

In addition, we originally talked about only including emerging markets with a Debt/GDP ratio above 
a threshold of 10% or 20%. To find out which ones those are, I first downloaded the Debt/GDP ratio of
all avaiable countries from the IMF's global debt database. 
https://www.imf.org/external/datamapper/CG_DEBT_GDP@GDD/FADGDWORLD
I chose the indicator "Central Government Debt" for e.o.y. 2018 as 2019 was not comprehensive. 
I saved the data to IMF.xls
Next, I checked which countries the IMF classifies as Emerging Markets as per October 2019. 
https://www.imf.org/~/media/Files/Publications/WEO/2019/October/English/text.ashx?la=en
p. 166 - 167 contains the list of countries classified as EM by the IMF. 
I hand-coded the EM classified countries as 1 in the IMF.xls sheet. All other countries are coded 0.


PRELIMINARY ANALYSIS

getting and seeting the working directory
getwd()
setwd("/Users/timodaehler/Desktop")

loading required packages
library(readxl)
library(dplyr)

importing the IMF.xls sheet, which contains all country for which Debt/GDP in 2018 is avaiable
imfDF <- read_excel("IMF.xls", sheet = 1)  

Format of debt ratio needs to be changed to numeric
imfDF$Debt <- as.numeric(imfDF$Debt) 

filtering for EM countries and creating dataframe that only contains emerging markets
EMOnlyDF <-  imfDF %>% filter(EM == 1) 

counting number of countries in dataframe
nrow(EMOnlyDF)
88 countries are classified as developing or emerging market

filtering for emerging markets with debt ratio above threshold
threshold <- 20
EMOnlyDF %>% filter(Debt > threshold)
77 of 88 EM countries have Debt/GDP above 20%. 

I increase the threshold to 50%
threshold <- 50
EMOnlyDF %>% filter(Debt > threshold)
41 of 88 EM countries have Debt/GDP above 20%. Many of them are countries from Africa, South America,
the Carribean or Central Asian. While there is of course some overlap, crucial countries such as
China, India, and Brazil would not be in the sample. I conclude that the EMBI constituents should
be used instead of a threshold approach. 

In the next step I visualize the EMBI countries.

Loading packages
library(rworldmap)

Creating the vector of the 31 countries in the EMBI
EMBICountries <- c("IDN", "MEX", "SAU", "RUS", "QAT", "PHL", "CHN", "TUR", "ARE", "BRA", "COL", "KAZ", "CHL", "ZAF", "PER", "PAN", "URY", "DOM", "EGY", "BHR", "OMN", "UKR", "MYS", "HUN", "LKA", "NGA", "POL", "GHA", "ARG", "AZE", "ROU")
Checking if there are 31 countries in the EMBI vector 
length(EMBICountries) == 31
Check result: positive

Creating the vector of the 3 countries I would add on top (India, Thailand, South Korea)
additionalCountries <- c("IND", "THA", "KOR")

Combining all countries
allCountries <- c(EMBICountries, theCountriesIWouldAdd)

allCountriesDF is a data.frame with the ISO3 country names plus a variable to
 merge to the map data. The variable is 1 for EMBI countries and 2 for additional countries
allCountriesDF <- data.frame(country = allCountries,
                             EMBI = c(rep.int(1, 31), rep.int(2,3))  )

 This will join the allCountriesDF data.frame to the country map data
allCountriesMap <- joinCountryData2Map(allCountriesDF, joinCode = "ISO3",
                                       nameJoinColumn = "country")

 And this will plot it, with the trick that the color palette's first
color is red
mapCountryData(allCountriesMap, nameColumnToPlot="EMBI", catMethod = "categorical",
               missingCountryCol = gray(.8), addLegend = FALSE)







