# PyBer Analysis

## Overview

PyBer, a python based ridesharing app company is aiming to improve rideshare services and determine affordability for underserved neighborhoods. The company has provided rideshare data from January to early May of 2019 on riders, drivers, and fares from a number of rural areas, suburban and urban cities. The analyses and visualization of the data will be presented to the CEO of the company to help in decision making.

## Resources

Data sources:
 - city_data.csv
 - ride_data.csv
 
Softwares:
 - Python 3.9.7
 - Conda 4.11.0
 - Jupyter Notebook 6.4.5

## Purpose

The purpose of the analyses is to summarize and visualize ridesharing data.

A summary dataframe will be created to understand the trends of ridesharing by city type, namely urban, suburban and rural. In addition to this, a line chart will be generated to visualize weekly total fares by different types of cities.

## Algorithm

The main steps in the analyses are as below:

- With Pandas and Matplotlib libraries, we read two csv files on City and Rides data. These datasets were then merged and following matrices were calculated:

1. Total rides by city type.
 
 ```
 rides_count = pyber_data_df.groupby(["type"]).count()["ride_id"]
 
 ```
2. Total drivers by city type.

```
drivers_count = city_data_df.groupby(["type"]).sum()["driver_count"]

```
3. Total amount of fares by city type.

```
fares_count = pyber_data_df.groupby(["type"]).sum()["fare"]

```
4. The average fare per ride by city type.

```
average_fare_per_ride = fares_count / rides_count

```
5. The average fare per driver by city type. 

```
average_fare_per_driver = fares_count / drivers_count

```
- With the above metrices, a summary dataframe was created and formatted.

- To calculate the fares by city type and date, a new dataframe was created by using groupby on city type and date. Next, the dataframe was pivoted on date and city type.

```
sum_of_fares_pivot =sum_of_fares.pivot(index="date",
                                       columns="type",
                                       values="fare")
                                     
```
- Using loc on the dates, a new dataframe was created for dates within '2019-01-01':'2019-04-28'.

- By setting the "date" index to datetime datatype and resampling the dataframe by week, a dataframe on weekly total fares by city type was created and visualized using a line graph.

```
weekly_fares = farecounts_Jan_April.resample('W').sum()

```

![Pivot_Fares]()

## Results

### Summary by city type

- According to the PyBer summary dataframe, between January and May in 2019, there were 1,625 rides in urban cities, 625 rides in suburban cities, and 125 rides in rural areas. Also there were 2,405 drivers in urban cities, 490 drivers in suburban cities and 78 drivers in rural areas.

![Pyber_Summary]()

- The above table shows that, both the number of total rides and drivers are higher in urban cities than suburban cities and rural area. Especially in urban cities, there was a larger number of drivers compared to rural areas. On the other hand, the average fare per ride are higher in rural areas than suburban and urban cities. The average fare per driver for suburban cities and rural areas are around 2.5 times and 3.5 times higher than urban cities, respectively.

- As urban cities have larger population, total fares, total rides, and total drivers are all quite high and, as a result, average fare per ride and per driver are less than their suburban and rural counterparts. By comparison, ridesharing services are most expensive in rural areas.

### Fares by city type

Below multiple-line chart shows total fares by city type:

![PyBer_fare_summary]()

- At any given time, total weekly fares in urban cities are higher than that of suburban cities, which is in turn higher than rural areas.

- For any city type, a spike in total weekly fares can be seen in the third week of february.

- The lines more or less show similar trajectories indicating that the pattern of ridesharing are similar regardless of city type. 

## Summary

To address the disparities in ridesharing services among different types of cities, following measures may be considered:

1. Discounts may be offred to riders in suburban cities and rural areas to reduce fare per ride. This may, in turn, increase ridership and drive down the fare.

2. Drivers in suburban cities and rural areas may be provided incentives through reduced commission. This will reduce the fare per ride and may increase availability of ridesharing services in these areas.

3. More data need to be acquired and further analyses need to be done to understand the pattern of ridesharing better. If the rides are geoloaction tagged, it will help understand which parts of the cities are better served and whether it aligns with the population density of areas in the cities. Also, it needs to be inverstigated whether the low volume of rides and total fares in the rural and suburban areas are exclusively due to fewer riders or lack of availability of service as well.
