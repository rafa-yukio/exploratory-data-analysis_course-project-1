# exploratory-data-analysis_course-project-1

# Number of rows
rows <- 2075259

# Number of columns
columns <- 9

# Numberic data has 8 bytes
bytes <- 8

# Calculating memory requeriments in bytes
memory_b <- rows * columns * bytes

# Calculating memory requeriments in Kilo bytes
memory_kb <- memory_b/(2^10)

# Calculating memory requeriments in Mega bytes
memory_Mb <- memory_kb/(2^10)

# References
# 
# * https://www.r-bloggers.com/2016/07/calculating-memory-requirements/
# * http://adv-r.had.co.nz/memory.html

# Printing the Memory Requirements
memory_Mb

# 1. Libraries used to perform this script. ####
library(lubridate)
library(tidyverse)
library(magrittr)

# 2. Creating a folder to store the downloaded files. ####
if(!file.exists("data")) {
    # If this folder already have been created, it will be ignored.
    dir.create("data")
}

# 3. Downloading the zip file with Electric power consumption from UC Irvine Machine Learning Repository. ####
if(!file.exists("./data/power_consumption.zip")) {
    
    # Download and store it in data folder.
    download.file(url = "https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip",
                  destfile = "./data/power_consumption.zip")
}

# 3.1. Unzipping the power_consumption file
if(!file.exists("./data/household_power_consumption.txt")) {
    
    # Check if the power_consumption.zip has been unzipped
    unzip(zipfile = "./data/power_consumption.zip",
          exdir = "./data",
          list = FALSE,
          overwrite = TRUE)
}

# 4. Loading the data ####
#
# Based on the instruction, we already know the types of the columns.
#
raw_dataset <- read.table(file = "./data/household_power_consumption.txt",
                          header = TRUE,
                          sep = ';',
                          stringsAsFactors = FALSE ,
                          na.strings = "?",
                          nrows = 2075259, 
                          check.names = FALSE,
                          colClasses = c(character(),
                                         character(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric()))

# 5. Manipulating Data ####

# 5.1. Converting the Date column into the Date class object and Filtering the observations
df_tidy <- raw_dataset %>%
    
    # Merging Date and Time POSIXlt.
    mutate(Time = strptime(paste(Date, " " ,Time), "%d/%m/%Y %H:%M:%S")) %>%
    
    # Converging character into Date.
    mutate(Date = as.Date(Date, "%d/%m/%Y")) %>%
    
    # Filtering observations between 2007-02-01 and 2007-02-02.
    filter(Date >= "2007-02-01" & Date <= "2007-02-02")

# 6. Exporting the PNG file ####
png(filename = "./plot1.png",   # The png file will be exported to the repository top-level
    width = 480 ,
    height = 480,
    units = "px",
    bg = "white")

    # Creating the histogram.
    hist(x = df_tidy$Global_active_power,
         col = "red",
         main = "Global Active Power",
         xlab = "Global Active Power (kW)")

dev.off()



# 1. Libraries used to perform this script. ####
library(lubridate)
library(tidyverse)
library(magrittr)

# 2. Creating a folder to store the downloaded files. ####
if(!file.exists("data")) {
    # If this folder already have been created, it will be ignored.
    dir.create("data")
}

# 3. Downloading the zip file with Electric power consumption from UC Irvine Machine Learning Repository. ####
if(!file.exists("./data/power_consumption.zip")) {
    
    # Download and store it in data folder.
    download.file(url = "https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip",
                  destfile = "./data/power_consumption.zip")
}

# 3.1. Unzipping the power_consumption file
if(!file.exists("./data/household_power_consumption.txt")) {
    
    # Check if the power_consumption.zip has been unzipped
    unzip(zipfile = "./data/power_consumption.zip",
          exdir = "./data",
          list = FALSE,
          overwrite = TRUE)
}

# 4. Loading the data ####
#
# Based on the instruction, we already know the types of the columns.
#
raw_dataset <- read.table(file = "./data/household_power_consumption.txt",
                          header = TRUE,
                          sep = ';',
                          stringsAsFactors = FALSE ,
                          na.strings = "?",
                          nrows = 2075259, 
                          check.names = FALSE,
                          colClasses = c(character(),
                                         character(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric()))

# 5. Manipulating Data ####

# 5.1. Converting the Date column into the Date class object and Filtering the observations
df_tidy <- raw_dataset %>%
    
    # Merging Date and Time POSIXlt.
    mutate(Time = strptime(paste(Date, " " ,Time), "%d/%m/%Y %H:%M:%S")) %>%
    
    # Converging character into Date.
    mutate(Date = as.Date(Date, "%d/%m/%Y")) %>%
    
    # Filtering observations between 2007-02-01 and 2007-02-02.
    filter(Date >= "2007-02-01" & Date <= "2007-02-02")

# 6. Exporting the PNG file ####
png(filename = "./plot2.png",
    width = 480 ,
    height = 480,
    units = "px",
    bg = "white")

    # Forcing to printing in English.
    Sys.setlocale("LC_TIME", "English")
    
    # Plotting the Graphic
    plot(df_tidy$Time,
         df_tidy$Global_active_power,
         type="l",
         xlab="",
         ylab="Global Active Power (kW)")

dev.off()








# 1. Libraries used to perform this script. ####
library(lubridate)
library(tidyverse)
library(magrittr)

# 2. Creating a folder to store the downloaded files. ####
if(!file.exists("data")) {
    # If this folder already have been created, it will be ignored.
    dir.create("data")
}

# 3. Downloading the zip file with Electric power consumption from UC Irvine Machine Learning Repository. ####
if(!file.exists("./data/power_consumption.zip")) {
    
    # Download and store it in data folder.
    download.file(url = "https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip",
                  destfile = "./data/power_consumption.zip")
}

# 3.1. Unzipping the power_consumption file
if(!file.exists("./data/household_power_consumption.txt")) {
    
    # Check if the power_consumption.zip has been unzipped
    unzip(zipfile = "./data/power_consumption.zip",
          exdir = "./data",
          list = FALSE,
          overwrite = TRUE)
}

# 4. Loading the data ####
#
# Based on the instruction, we already know the types of the columns.
#
raw_dataset <- read.table(file = "./data/household_power_consumption.txt",
                          header = TRUE,
                          sep = ';',
                          stringsAsFactors = FALSE ,
                          na.strings = "?",
                          nrows = 2075259, 
                          check.names = FALSE,
                          colClasses = c(character(),
                                         character(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric()))

# 5. Manipulating Data ####

# 5.1. Converting the Date column into the Date class object and Filtering the observations
df_tidy <- raw_dataset %>%
    
    # Merging Date and Time POSIXlt.
    mutate(Time = strptime(paste(Date, " " ,Time), "%d/%m/%Y %H:%M:%S")) %>%
    
    # Converging character into Date.
    mutate(Date = as.Date(Date, "%d/%m/%Y")) %>%
    
    # Filtering observations between 2007-02-01 and 2007-02-02.
    filter(Date >= "2007-02-01" & Date <= "2007-02-02")

# 6. Exporting the PNG file ####
png(filename = "./plot3.png",
    width = 480 ,
    height = 480,
    units = "px",
    bg = "white")

    # Forcing to printing in English.
    Sys.setlocale("LC_TIME", "English")

    plot(x = df_tidy$Time,
         y = df_tidy$Sub_metering_1,
         type = "l",
         ylab = "Energy sub metering",
         xlab = "")
    
    lines(x = df_tidy$Time,
          y = df_tidy$Sub_metering_2,
          type = "l",
          col = "red")
    
    lines(x = df_tidy$Time,
          y = df_tidy$Sub_metering_3,
          type = "l",
          col = "blue")
    
    legend(x = "topright",
           legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"),
           lty = 1,
           lwd = 2.5,
           col=c("black", "red", "blue"))

dev.off()



# 1. Libraries used to perform this script. ####
library(lubridate)
library(tidyverse)
library(magrittr)

# 2. Creating a folder to store the downloaded files. ####
if(!file.exists("data")) {
    # If this folder already have been created, it will be ignored.
    dir.create("data")
}

# 3. Downloading the zip file with Electric power consumption from UC Irvine Machine Learning Repository. ####
if(!file.exists("./data/power_consumption.zip")) {
    
    # Download and store it in data folder.
    download.file(url = "https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip",
                  destfile = "./data/power_consumption.zip")
}

# 3.1. Unzipping the power_consumption file
if(!file.exists("./data/household_power_consumption.txt")) {
    
    # Check if the power_consumption.zip has been unzipped
    unzip(zipfile = "./data/power_consumption.zip",
          exdir = "./data",
          list = FALSE,
          overwrite = TRUE)
}

# 4. Loading the data ####
#
# Based on the instruction, we already know the types of the columns.
#
raw_dataset <- read.table(file = "./data/household_power_consumption.txt",
                          header = TRUE,
                          sep = ';',
                          stringsAsFactors = FALSE ,
                          na.strings = "?",
                          nrows = 2075259, 
                          check.names = FALSE,
                          colClasses = c(character(),
                                         character(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric(),
                                         numeric()))

# 5. Manipulating Data ####

# 5.1. Converting the Date column into the Date class object and Filtering the observations
df_tidy <- raw_dataset %>%
    
    # Merging Date and Time POSIXlt.
    mutate(Time = strptime(paste(Date, " " ,Time), "%d/%m/%Y %H:%M:%S")) %>%
    
    # Converging character into Date.
    mutate(Date = as.Date(Date, "%d/%m/%Y")) %>%
    
    # Filtering observations between 2007-02-01 and 2007-02-02.
    filter(Date >= "2007-02-01" & Date <= "2007-02-02")

# 6. Exporting the PNG file ####
png(filename = "./plot4.png",
    width = 480 ,
    height = 480,
    units = "px",
    bg = "white")

    # Forcing to printing in English.
    Sys.setlocale("LC_TIME", "English")
    
    # Create 4 fields to be filled with 4 plots
    par(mfrow = c(2, 2))
    
    # Top-left
    plot(x = df_tidy$Time,
         y = df_tidy$Global_active_power ,
         type = "l",
         xlab = "",
         ylab = "Global Active Power")
    
    ## Top-right
    plot(x = df_tidy$Time,
         y = df_tidy$Voltage ,
         type = "l",
         xlab = "datetime",
         ylab = "Voltage")
    
    ## Bottom-left
    plot(x = df_tidy$Time,
         y = df_tidy$Sub_metering_1,
         type = "l",
         ylab = "Energy sub metering",
         xlab = "")
    
    lines(x = df_tidy$Time, 
          y = df_tidy$Sub_metering_2, 
          type = "l", 
          col = "red")
    
    lines(x = df_tidy$Time, 
          y = df_tidy$Sub_metering_3, 
          type = "l",
          col = "blue")
    
    legend(x = "topright",
           legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"),
           lty = 1,
           lwd = 2.5,
           col=c("black", "red", "blue"),
           bty="n")
    
    ## Bottom-right
    plot(x = df_tidy$Time,
         y = df_tidy$Global_reactive_power,
         type = "l",
         col = "black",
         xlab = "datetime",
         ylab = "Global_reactive_power")

dev.off()
