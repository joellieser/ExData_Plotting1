# README
## This object contains the following:

* Description of the Assignment
* Script Information
* Code Explanation
* Instructions for Executing

## Description of the Assignment
#### Taken from https://class.coursera.org/exdata-004/human_grading/view/courses/972141/assessments/3/

This assignment uses data from the UC Irvine Machine Learning Repository, a popular repository for machine learning datasets. In particular, we will be using the “Individual household electric power consumption Data Set” which I have made available on the course web site:


Dataset: Electric power consumption [20Mb]


Description: Measurements of electric power consumption in one household with a one-minute sampling rate over a period of almost 4 years. Different electrical quantities and some sub-metering values are available.


The following descriptions of the 9 variables in the dataset are taken from the UCI web site:


Date: Date in format dd/mm/yyyy
Time: time in format hh:mm:ss
Global_active_power: household global minute-averaged active power (in kilowatt)
Global_reactive_power: household global minute-averaged reactive power (in kilowatt)
Voltage: minute-averaged voltage (in volt)
Global_intensity: household global minute-averaged current intensity (in ampere)
Sub_metering_1: energy sub-metering No. 1 (in watt-hour of active energy). It corresponds to the kitchen, containing mainly a dishwasher, an oven and a microwave (hot plates are not electric but gas powered).
Sub_metering_2: energy sub-metering No. 2 (in watt-hour of active energy). It corresponds to the laundry room, containing a washing-machine, a tumble-drier, a refrigerator and a light.
Sub_metering_3: energy sub-metering No. 3 (in watt-hour of active energy). It corresponds to an electric water-heater and an air-conditioner.

## Script Information
There are four (4) scripts contained in this branch:

* plot1.R
* plot2.R
* plot3.R
* plot4.R

## Code Explanation
All four scripts contain a set of shared code, as shown below (with comments describing what the following line does:
#### open png plotting device
png("plotX.png") ### Where X in plotX.png is a value 1, 2, 3 or 4
#### read input data
ip <- read.table("household_power_consumption.txt",sep=";",header=TRUE,na.strings="?")
#### filter out only required data
ip_filt <- subset(ip,Date == '1/2/2007' | Date == '2/2/2007')
#### free up memory used by ip
ip <- NULL
#### concat date and time columns
ip_filt$DtTm <- paste(ip_filt$Date,ip_filt$Time,sep=" ")
#### cast as datetime type
ip_filt$DtTm <- strptime(ip_filt$DtTm, format="%d/%m/%Y %H:%M:%S")
#### create plot

The step following the shared code block is specific for each section of the assignment and is broken out by script.
### plot1.R
hist(ip_filt$Global_active_power, main="Global Active Power", xlab="Global Active Power (kilowatts)", ylab="Frequency",col="red")

### plot2.R
with(ip_filt,plot(ip_filt$DtTm,ip_filt$Global_active_power, type = "l", ylab="Global Active Power (kilowatts)", xlab = "", main=""))

### plot3.R
plot(ip_filt$DtTm,ip_filt$Sub_metering_1, type = "l",col="black", ylab="Energy sub metering", xlab = "", main="")
points(ip_filt$DtTm,ip_filt$Sub_metering_2, type = "l",col="red")
points(ip_filt$DtTm,ip_filt$Sub_metering_3, type = "l",col="blue")
legend("topright",c("Sub_metering_1","Sub_metering_2","Sub_metering_3"),lty = c(1, 1, 1),col=c("black","red","blue"))

### plot4.R
#### create plot (2 rows, 2 columns)
par(mfrow=c(2,2))
####upper left
with(ip_filt,plot(ip_filt$DtTm,ip_filt$Global_active_power, type = "l", ylab="Global Active Power", xlab = "", main=""))
####upper right
with(ip_filt,plot(ip_filt$DtTm,ip_filt$Voltage, type = "l", ylab="Voltage", xlab = "", main=""))
####lower left
plot(ip_filt$DtTm,ip_filt$Sub_metering_1, type = "l",col="black", ylab="Energy sub metering", xlab = "", main="")
points(ip_filt$DtTm,ip_filt$Sub_metering_2, type = "l",col="red")
points(ip_filt$DtTm,ip_filt$Sub_metering_3, type = "l",col="blue")
legend("topright",bty="n",c("Sub_metering_1","Sub_metering_2","Sub_metering_3"),lty = c(1, 1, 1),col=c("black","red","blue"))
####lower right
with(ip_filt,plot(ip_filt$DtTm,ip_filt$Global_reactive_power, type = "l", ylab="Global_reactive_power", xlab = "datetime", main=""))

All scripts end by closing the png device using the following code:

#### close device
dev.off()

## Execution Information
#### set working directory to location of input data
#### execute code, as shown below
#### Note: Your working directory (and thus, first line below) may differ 
> setwd("~/Desktop/Data Science Track/4 - Exploratory Data Analysis/Assignment 1")

> source("plot1.R")

> source("plot2.R")

> source("plot3.R")

> source("plot4.R")

#### The resulting .png files are stored in the working directory where the source data is located.
