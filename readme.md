# Team-Project-1

**Partner names:**

## Data
The data `MonthlyWeather.csv` contain monthly weather readings for 113 US airports from July, 2014 through September, 2017. Variable descriptions are given below. The location of this data is https://raw.githubusercontent.com/mgelman/data/master/MonthlyWeather.csv. 

## To do:
Use `ggplot2` to create graphs that can answer the following questions. For each set of questions, create 1-2 graphs and use the graphs to answer the questions in a paragraph or two. You will be graded on the appropriateness and originality of your graphs, explanation/interpretation, and the readability of your R code.

1. Suppose you don't like big daily temperature swings and cloudy days. Which month(s) or time of year have the most consistent daily temps? the most variable daily temps? Which month(s) or time of year have the most sunny days? the fewest sunny days?
2. Consider 2016 weather data. Which regions or states  have the most consistent daily temps? the most variable daily temps? Which regions or states have the most sunny days? the fewest sunny days?
3. What criteria are important to you for choosing a city to live in? Create some figures that help determine which city you would live in based on that criteria. Would you choose one particular city to live in year round or would you migrate to different locations depending on the season?

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

