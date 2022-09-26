# Team-Project-1

**Partner names: Abizer Mamnoon, Luis Gomez**

## Data
The data `MonthlyWeather.csv` contain monthly weather readings for 113 US airports from July, 2014 through September, 2017. Variable descriptions are given below. The location of this data is https://raw.githubusercontent.com/mgelman/data/master/MonthlyWeather.csv. 

## To do:
Use `ggplot2` to create graphs that can answer the following questions. For each set of questions, create 1-2 graphs and use the graphs to answer the questions in a paragraph or two. You will be graded on the appropriateness and originality of your graphs, explanation/interpretation, and the readability of your R code.

```{r include=FALSE}
MonthlyWeather <- read.csv("https://raw.githubusercontent.com/mgelman/data/master/MonthlyWeather.csv")
library(ggplot2)
library(dplyr)
glimpse(MonthlyWeather)
```

1. Suppose you don't like big daily temperature swings and cloudy days. Which month(s) or time of year have the most consistent daily temps? the most variable daily temps? Which month(s) or time of year have the most sunny days? the fewest sunny days?

#The code below depicts a bar graph of the average temperature range vs. months. The bar graph is arranged in decending order from the month with the highest temperature range to the lowest. 
```{r echo = FALSE}
library(ggplot2)
library(dplyr)
Consistent <- MonthlyWeather %>% select(month,year,avgTmpDiffF)  %>% group_by(month) %>% summarize(mn = round(mean(avgTmpDiffF),2))%>% arrange(mn)
Consistent %>% ggplot(aes(x = reorder(month,mn), y = mn-15)) + geom_bar(stat = 'identity')  + coord_flip() + xlab("Months") + ylab("Average Temperature Range (F) -15 ") + ggtitle("Average Temperature Range per Month")
```

December has the most consistent daily temperature as the average of the daily max - min temperature in June is the lowest at 16.1 degrees F. June has the most variable daily temperatures as the average of the daily max - min temperature in June is the highest at 22.4 degrees F.Based on the graph, September is somewhat of an outliar since it is equal to 0. 


#The code below depicts a bar graph of the mean number of sunny day vs. months. The bar graph is arranged in decending order from the month with the most days of sunny days to the lowest.
```{r echo = FALSE}
library(ggplot2)
library(dplyr)
Sunny <- MonthlyWeather %>% select(month,year,numSunDay)  %>% group_by(month) %>% summarize(mn = round(mean(numSunDay),2)) %>% arrange(desc(mn))
Sunny %>% ggplot(aes(x = reorder(month,mn), y = mn - 5)) + geom_bar(stat = 'identity') + coord_flip() + xlab("Months") + ylab("Mean Number of Sunny Days - 5") + ggtitle("Average Number of Sunny Days per Month")
```

December has on average 8.4 sunny days which is the lowest average number of sunny days a month has in the year. July has on average 15.3 sunny days which is the highest average number of sunny days a month has in the year.

2. Consider 2016 weather data. Which regions or states  have the most consistent daily temps? the most variable daily temps? Which regions or states have the most sunny days? the fewest sunny days?


#The code below depicts a map of the US and its average temperature range in 2016. Each US state in the map is colored with a shade of orange that represents a temperature range. The higher the number, the darker the shade of orange the state will be.   
```{r echo = FALSE}
library(ggplot2)
MonthlyWeather$state <- tolower(MonthlyWeather$state)
Temps <- MonthlyWeather %>% select(year,avgTmpDiffF,state,city,longitude,latitude) %>% filter(year == 2016) %>% group_by(state) %>% summarize(mn = round(mean(avgTmpDiffF),2))%>% arrange(mn)
MainStates <- map_data("state")
ggplot() + coord_quickmap() + geom_map(data = Temps, aes(map_id = state, fill = mn), map = MainStates) + expand_limits(x = MainStates$long, y = MainStates$lat) + ggtitle(" 2016 Average Range of Temperatures in US States") + scale_fill_distiller(palette = "Oranges")
```

States in the East have more consistent temperatures than states in the West.There are more variable sunny days in the West. Florida is the state with the lowest average temperature range while New Mexico is state with the most highest average temperature range. 



#The code below depicts a map of the US and its average number of sunny days range in 2016. Each US state in the map is colored with a shade of purple that represents a number of sunny days. The higher the number, the darker the shade of purple the state will be.   
```{r echo = FALSE}
library(ggplot2)
MonthlyWeather$state <- tolower(MonthlyWeather$state)
Temps <- MonthlyWeather %>% select(year,numSunDay ,state,city,longitude,latitude) %>% filter(year == 2016) %>% group_by(state) %>% summarize(mn = round(mean(numSunDay),2))%>% arrange(mn)
MainStates <- map_data("state")
ggplot() + coord_quickmap() + geom_map(data = Temps, aes(map_id = state, fill = mn), map = MainStates) + expand_limits(x = MainStates$long, y = MainStates$lat) + ggtitle(" 2016 Average Number of Sunny Days in US States") + scale_fill_gradient(low = "lightpink", high = "purple4")
```
States in the central part of the US tend to have more sunny days. While states in the midwest and North East tend to have the least number of sunny days. New Mexico has the most average number of sunny days while a state in the North East is the state with the lowest number of sunny days.  

3. What criteria are important to you for choosing a city to live in? Create some figures that help determine which city you would live in based on that criteria. Would you choose one particular city to live in year round or would you migrate to different locations depending on the season?


```{r echo = FALSE}
library(ggplot2)
library(dplyr)
MonthlyWeather$state <-tolower(MonthlyWeather$state)

Temps <- MonthlyWeather %>% select(year,avgMaxTmpF,avgMinTmpF ,avgPrecipIn,avgWindMPH,state,city,longitude,latitude) %>% filter(year == 2016) %>% group_by(state) %>% summarize(max_temp = round(mean(avgMaxTmpF),2), min_temp = round(mean(avgMinTmpF),2), rain = round(mean(avgPrecipIn),2), wind_speed = round(mean(avgWindMPH),2)) %>% mutate(min_temp_point = ifelse(min_temp > 60 & min_temp <= 70, 2, 1), rain_point = ifelse(rain < 0.05, 2,1), wind_point = ifelse(wind_speed < 12, 2, 1), cum = min_temp - 300*rain - wind_speed)

```



#The code below depicts a map of the US and its average number of sunny days range in 2016. Each US state in the map is colored with a shade of blue that represents a number of average minimum temperature. The higher the number, the darker the shade of blue the state will be.

```{r echo = FALSE}
MainStates <- map_data("state")
ggplot() + coord_quickmap() + geom_map(data = Temps, aes(map_id = state, fill = min_temp), map = MainStates) + expand_limits(x = MainStates$long, y = MainStates$lat) + ggtitle(" 2016 Average Minimum Temperature in US States") + scale_fill_distiller()
```
States in the Northern part of the US tend to have a lower average number of minimum temperature while states in the south tend to have a higher average number of temperature. 


#The code below depicts a map of the US and its average number of percipitation in 2016. Each US state in the map is colored with a shade of blue that represents a number of amount of percipitation. The higher the number, the darker the shade of blue the state will be.
```{r echo = FALSE}
MainStates <- map_data("state")
ggplot() + coord_quickmap() + geom_map(data = Temps, aes(map_id = state, fill = rain), map = MainStates) + expand_limits(x = MainStates$long, y = MainStates$lat) + ggtitle(" 2016 Average Precipitation in US States") + scale_fill_distiller()
```
States in the south west part of the US tend to have the most average amount of precipitation, with Louisiana having the most. States in the Western part of the US tend to have the least amount of precipitation. 


#The code below depicts a map of the US and its average number of wind speed in 2016. Each US state in the map is colored with a shade of blue that represents a number of wind speed. The higher the number, the darker the shade of blue the state will be.
```{r echo = FALSE}
MainStates <- map_data("state")
ggplot() + coord_quickmap() + geom_map(data = Temps, aes(map_id = state, fill = wind_speed), map = MainStates) + expand_limits(x = MainStates$long, y = MainStates$lat) + ggtitle(" 2016 Average Wind Speed in US States") + scale_fill_distiller()
```
States around Arkansas tend to have lower wind speeds. The place with the most wind speed is Wyioming. 



```{r echo = FALSE}
MainStates <- map_data("state")
Temps <- arrange(Temps, desc(cum)) 
Temps[1:10,] %>% ggplot(aes(x = reorder(state,cum), y = cum )) + geom_bar(stat = 'identity') + coord_flip() + xlab("States") + ylab("Cumulative Score") + ggtitle("Ranking of States") + geom_text(aes(label = cum),nudge_y = 2, size = 2)
```
The equation we came up with goes as follows: as minimum temperature increases the rating increases, for wind speed there is a negative relation as the higher the wind speed the lower the rating, for rain we multiplied the variable by 300 in order to make it the same range as the rest (also negative relation). According to our bar graph, Hawaii is the best place to live in. 


## Turn in:
Push your .Rmd and .md to GitHub by Tue, Sep. 27 11:59PM. Hide all code in your knitted doc so I just see graphs, interpretations, and section headers for each part. 

## Variables:

- `avgMinTmpF` and `avgMaxTmpF` average of daily max or min temps
- `minTmpF` and `maxTmpF` monthly min or max temps 
- `avgTmpF` average temp 
- `avgTmpDiffF` mean of daily max - min temps
- `avgPrecipIn` average daily precipitation (inches)
- `maxWindMPH` monthly max sustained wind speed
- `avgWindMPH` average of daily max sustained wind speed
- `numSunDay` number of days that are clear/mostly sunny
- `numDay` number of measured days 
- `AirPtCd` airport code
- `city` closest city to the airport
- `state` location of airport
- `latitude`, `longitude`
- `month`, `year`

## Grading: 66 points possible (22/part)

Each part above (1-3) will have a score determined by:
score = 2*correctness + design + presentation + style

5 point scale for 

- correctness: does code work and produce results that address the desired goal
- design and originality: does the graph effectively display information and provide context, and/or does it convey info in a unique way
- presentation: does your written explanation effectively motivate and explain your analysis  
  - 5 = best, basically no room for improvement
  - 4 = better, minor room for improvement
  - 3 = good, some room for improvement
  - 2 = fair, ample room for improvement
  - 1 = poor, did not finish
  - 0 = no attempt

Two-point scale for

- style and readability: is the code readable and appropriately commented
  - 2 = readable and sufficient comments
  - 1 = mostly readable but contains one or more portions that could be written in a more clear manner
  - 0 = most code could be written in a more readable manner 
