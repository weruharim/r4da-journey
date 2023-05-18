# r4da-journey

##Table of Contents
- [Introduction](##introduction)
- [Data Visualisatin Using R](##data-visualisation-using-r)
- [Prerequisites](### Prerequisites)
- [Examples of visualisation with Scatter Plot](### Examples of visualisation with Scatter Plot)
- [Faceting](### Faceting)
- [Other Plot Types](### Other Plot Types)
- [Data Transformation](## Data Transformation)
- [Filtering data using `filter()` function in R](### Filtering data using `filter()` function in R)
- [Arranging data using `arrange()` function in R](### Arranging data using `arrange()` function in R)
- [Selecting data with the `select()` function in R](### Selecting data with the `select()` function in R)
- [Adding New Variables With `mutate()` in R](### Adding New Variables With `mutate()` in R)

## Introduction
My journey of learning R For Data Analysis using R for Data Science book by Hadley Wickham and Garrett Grolemund (2017). The book is freely accessible from https://r4ds.had.co.nz/

## Data Visualisation Using R
This documentation provides examples that I used to learn data visualization techniques in R. The code snippets and explanations below demonstrate how I created various plot types and customization options.

### Prerequisites
Before running the code, I made sure I have the `tidyverse` package installed. I installed it using the following command in R:

```R
install.packages("tidyverse")
```

I will use the mpg data frame that comes with ggplot2 to demonstrate what I have learned from the book.

### Examples of visualisation with Scatter Plot
To create a scatter plot, I used the geom_point() function from the ggplot2 package. The example below plots the displ (displacement) on the x-axis and hwy (highway miles per gallon) on the y-axis.
```R
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy))
```

#### Customizing Scatter Plots
I added properties to the aesthetic (aes()) such as colour, shape, size, and alpha to differentiate the plots. Here are a few examples:

```R
# Coloring the points by class
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, colour = class))

# Varying transparency of points by class
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, alpha = class))

# Varying the size of points by class
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, size = class))

# Using different shapes for points by class
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```
#### Manually Setting Aesthetic Properties
I also learned that the aes properties of the scatter plot can be set mannually. 

##### Changing Point Colour
To change the point colour manually, I used the colour parameter outside aes(). Here's an example:
```R
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), colour = "yellow")
  ```

To change the point size manually, I used the size parameter outside aes(). Here's an example:
```R
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), size = 3)
 ```

To change the point shape manually, I used the shape parameter outside aes(). Here's an example:
 ```R
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), shape = 24)
  ```
  #### Combining Aesthetic Properties
  ```R
##For shape 0-14, there is no fill. The colour is for the border.
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), colour = "green", shape = 2, size = 3)
##For shape 15-20, set the colour is for both the border and fill
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), colour = "green", shape = 17, size = 3)
##For shape 21-24, set both the colour for the border and the fill
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy), colour = "green", shape = 24, size = 3, fill = "yellow")
```

### Faceting
Faceting allows an analyst to create subplots for categorical data. I used facet_wrap() and facet_grid() functions to achieve this.
```R
# Faceting with facet_wrap() for a single variable (class)
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_wrap(~ class, nrow = 2)

# Faceting with facet_grid() for two variables (drv and cyl)
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ cyl)

# Faceting without specifying rows or columns
ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)

ggplot(data = mpg) +
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```

### Other Plot Types
Here are a few examples of other plot types that I created using R:

#### Smooth Chart

To create a smooth chart, use the geom_smooth() function. Here's an example:

```R
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy))
```
#### Boxplot

To create a boxplot, use the geom_boxplot() function. Here's an example:

```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_boxplot()
```

#### Line Chart
To create a line chart, use the geom_line() function. Here's an example:
```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_line()
```

#### Area Chart

To create an area chart, use the geom_area() function. Here's an example:

```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_area()
```
#### Histogram

To create a histogram, use the geom_histogram() function. Here's an example:

```R
ggplot(data = mpg, mapping = aes(x = displ)) +
  geom_histogram(binwidth = 1)
```

## Data Transformation
### Filtering data using `filter()` function in R
In my data analysis journey with R, I have learned how to use the `filter()` function to extract specific rows from a dataset based on certain conditions.

To begin, I loaded the necessary libraries, including the `tidyverse` and `nycflights13` packages. I also loaded the flights dataset from the `nycflights13` package to work with. This dataset contains information about flights that department New York in 2013.

To get a better understanding of the dataset, I used the `view()` function to see the entire flights data frame. Additionally, I explored the documentation for the `flights` dataset using the `?flights` command.

To filter the data and extract specific flights, I utilized the `filter()` function. For example, I filtered the flights dataset to extract flights that occurred on January 1st by specifying the conditions `month == 1` and `day == 1`. I stored the filtered data in a new data frame called `jan1`.
```R
jan1 <- filter(flights, month == 1, day == 1)
view(jan1)
```

To view the `jan1` data frame, I used the `view()` function again. Alternatively, I could print the new data frame by enclosing the assignment in parentheses, like this:

```R
(jan1 <- filter(flights, month == 1, day == 1))
```

Next, I experimented with filtering the flights dataset using comparison operators. I filtered flights with a an early departure of more than or equal to 20 minutes by applying the condition `dep_delay <= -20`. Similarly, I filtered flights with an air time of 60 minutes or more using the condition `air_time >= 60`.

```R
depDelayed <- filter(flights, dep_delay <= -20)
view(depDelayed)

longFlights <- filter(flights, air_time >= 60)
view(longFlights)
```

I also explored the use of Boolean operators to filter data based on multiple conditions. For instance, I filtered flights that occurred in October, November, or December and covered a distance of over 1000 miles. I achieved this by combining the conditions `(month %in% c(10, 11, 12))` and `distance > 1000`.

```R
peakLongFlights0 <- filter(flights, (month == 10 | month == 11 | month == 12) & distance >= 1000)
view(peakLongFlights)

#A simplified code
peakLongFlights <- filter(flights, (month %in% c(10,11,12)) & distance > 1000) 
```

In addition to the examples above, I completed a series of exercises to further practice filtering data using the `filter()` function. These exercises involved filtering flights based on various criteria such as arrival delay, destination, operating airline, departure month, and more. For each exercise, I used the `filter()` function with the corresponding conditions and stored the filtered data in new data frames. To examine the results, I utilized the `view()` function to inspect each filtered data frame.

```R
#Exercises
#Had an arrival delay of two or more hours
longDelays <- filter(flights, arr_delay >= 120)
view(longDelays)

#Flew to Houston (IAH or HOU)
flightsToHouston <- filter(flights, dest %in% c("IAH", "HOU"))
view(flightsToHouston)

#Were operated by United, American, or Delta
flightsOperated <- filter(flights, carrier %in% c("AA", "DL", "UA"))
view(flightsOperated)

#Departed in summer (July, August, and September)
summerFlights <- filter(flights, month %in% c(7, 8, 9))
view(summerFlights)  

#Arrived more than two hours late, but didn’t leave late
arrLateDepEarly <- filter(flights, arr_delay > 120 & dep_delay == 0)
view(arrLateDepEarly)

#Were delayed by at least an hour, but made up over 30 minutes in flight
longDelayed <- filter(flights, dep_delay > 60 & air_time > 30)
view(longDelayed)

#Departed between midnight and 6am (inclusive)
lateDep <- filter(flights, dep_time >= 2400 | dep_time <=6)
view(lateDep)
```

Throughout my learning process, I also discovered the usefulness of the `between()` helper function. I utilized this function to filter flights that occurred in the summer months (July, August, and September) and flights that departed between midnight and 6 am.

```R
#using between()
summerFlights1 <- filter(flights,  between(month, 7, 9))

lateDep1 <- filter(flights,  between(dep_time, 0, 6))
```

Lastly, I explored the concept of missing values and filtered flights that had a missing departure time using the `is.na()` function.

```R
#How many flights have a missing depature time?
missingDepTime <- filter(flights, is.na(dep_time))
view(missingDepTime)
```

By applying the `filter()` function and exploring various conditions and operators, I gained a better understanding of how to extract specific subsets of data from a larger dataset.


### Arranging data using `arrange()` function in R

When working with the `arrange()` function, I learned how to sort the flights based on different criteria:

To arrange the flights from the least delayed in arrival to the most delayed, I used the `arrange()` function with the `arr_delay` column.

```R
arrangedByArrDel <- arrange(flights, arr_delay)
```

To sort the flights from the most delayed in arrival to the least delayed, I used the `arrange()` function with the `desc()` helper function applied to the `arr_delay` column.

```R
delayedFlights <- arrange(flights, desc(arr_delay))
view(delayedFlights)
```
I completed a series of exercises to further practice arranging data using the `arrange()` function. For the exercises, I explored different sorting scenarios using `arrange()`:

I sorted the flights to bring all missing values to the start by applying the `desc()` helper function to the `is.na(dep_time)` expression.

```R
missingDepTime <- arrange(flights, desc(is.na(dep_time)))
```

To find the most delayed flights, I sorted the flights in descending order based on the departure delay (`dep_delay`) and arrival delay (`arr_delay`) columns.

```R
delayedDepFlight <- arrange(flights, desc(dep_delay))

delayedArrFlights <- arrange(flights, desc(arr_delay))
```

I identified the flights that left earliest by arranging the flights based on the departure delay (`dep_delay`) column.

```R
earlyDepFlights <- arrange(flights, dep_delay)
```

For finding the fastest flights, I used the `arrange()` function with the `air_time` column.

```R
fastFlights <- arrange(flights, air_time)
```

To determine which flights traveled the longest and shortest distances, I sorted the flights in descending order based on the distance column for the longest flights, and in ascending order for the shortest flights.

```R
#Which flights traveled the longest?
longFlights <- arrange(flights, desc(distance))

#Which traveled the shortest?
shortFlights <- arrange(flights, distance)
```

### Selecting data with the `select()` function in R

While working with the `select()` function, I learned how to choose specific variables from the flights data frame:

I selected only the destination column by using the `select()` function with the `dest` variable.

To extract a range of variables, I utilized the `select()` function with the range specified using the `: operator`.

Excluding specific variables from the selection was achieved by using the `-(variable_name)` notation within the `select()` function.

By employing helper functions like `contains()`, `starts_with()`, and `ends_with()`, I could select variables based on specific patterns in their names.

I also discovered the `rename()` function (a variation of `select()`, which allowed me to rename variables within the flights data frame.

I also conducted some exercises to practice different selection scenarios using `select()`:

I brainstormed multiple ways to select the `dep_time`, `dep_delay`, `arr_time`, and `arr_delay` variables from the flights data frame.

I explored the behavior of including the same variable multiple times in a `select()` call.

I learned about the `all_of()` and `any_of()` functions, which proved helpful when combined with a vector of variable names for selection.

I also experimented with the case sensitivity of select helpers and learned how to change the default behavior using the `ignore.case` argument within the helper functions.

### Adding New Variables With `mutate()` in R

```R
flightsSml <- select(
  flights,
  year:day,
  ends_with("delay"),
  distance,
  air_time
)
```

```R
mutate(flightsSml,
  gain = arr_delay - dep_delay,
  speed = distance/ air_time * 60
)
````
I also learned that I can  refer to a variable I have created

```R
calcFlightsSml <- mutate(flightsSml,
       gain = arr_delay - dep_delay,
       hours = air_time * 60,
       gainPerHour = gain / hours
       )
```
I discovered that variables created using `mutate()` are not kept. The `transmute()` function can be used to keep them instead of keeping all the variable.


```R
transmute(flightsSml,
       gain = arr_delay - dep_delay,
       speed = distance/ air_time * 60
)
```

I used modular arithmetic to breakdown time in hours and minutes

```R
transmute(
  flights,
  dep_hr = dep_time %/% 100,#dividing departure time by 100
  dep_min = dep_time %% 100 #storing the remainder of the above as minutes
)
```
I also learned to use `min_rank()` to rank values in a vector.

```R
x <- c(3, 2, 1, 1, 2, 2, 1, 1, 1)
min_rank(x)
````

I completed some exercises to test what I have learned. In the first exercise, I converted `dep_time` and `sched_dep_time` to a more convenient representation of number of minutes since midnight:

```R
flights <- mutate(flights,
                  dep_time_min = dep_time %/% 100 * 60 + dep_time %% 100,
                  sched_dep_time_min = sched_dep_time %/% 100 * 60 + sched_dep_time %% 100
                  )
 ```

Another exercise I did was to compare `air_time` with `arr_time - dep_time`. I created a new variable `air_time_calc` to refer to ``arr_time` - `dep_time``.

```R
flights <- mutate(flights,
                  air_time_calc = arr_time - dep_time
                  )
```

Looking at the first 10 rows, the two fields (`air_time_calc` and `air_time`) have different values. I thought the difference was because `arr_time` and `dep_time` are in HHMM format while `air_time` was in minutes. So I used `mutate()` to transform `arr_time` and `dep_time` to minutes.

```R
flights <- mutate(flights,
                  arr_time_min = arr_time %/% 100 * 60 + arr_time %% 100, #arrival time in minutes
                  dep_time_min = dep_time %/% 100 * 60 + dep_time %% 100, #departure time in minutes
                  air_time_calc1 = arr_time_min - dep_time_min #creating new air_time_calc field
                  )
```

Looking at the first 10 rows, the two fields their values are still different. The problem might be due to 
  1. Data errors 
  2. The flights passed midnight 
  3. Airports in different timezones

To check the first problem, I turned to the documentation and found out I did not miss anything. So I did a little research about the errors and found that it may be because of unaccounted time for taxiing, landing, and takeoff. This time which can vary significantly might explain why `air_time_calc1` is greater than `air_time` in most of the cases because the `arr_time` and `dep_time` include time for taxiing, landing, and takeoff. [Click here for more information](https://travel.stackexchange.com/questions/107373/is-departure-time-when-the-plane-leaves-the-gate-or-when-it-takes-off)

On the second problem, if the flight passed midnight, there could be a 1,440 minutes difference (24 hours). I used `filter()` to check this and found 5 flights with with this problem. I used the following code:

```R
flightsPassedMid <- flights %>% 
  filter(abs(air_time_calc1 - air_time) == 1440) #checking the absolute value of the difference
head(flightsPassedMid)
```

So what about the other flights? Can the final reason explain this? To get a clear picture of the problem, I printed a sample data of `air_time` and `air_time_calc1` fields together with `origin` and `dest` fields.

```R
sampleRows <- sample(nrow(flights), 20)  # Select 20 random rows
selectedCols <- c("origin", "dest","air_time", "air_time_calc1")  # Columns of interest
sampleData <- flights[sampleRows, selectedCols]
print(sampleData)
````

Then, I used `mutate()` to add a field for the differences between `air_time_calc1` and `air_time`


```R
sampleData <- mutate(sampleData, 
                     air_time_diff = air_time_calc1 - air_time
                     )
```
I hypothesized that flights between airports that are in different timezones might have `air_time_calc1` less than `air_time`. To prove my hypothesis, I used the `airports` data frame (part of `nycflights13` package). In the `airports` data frame, I selected the FAA airport code (`faa`). timezone (`tz`) and Daylight savings time zone (`dst`) for `origin` column. (Refer to the documentation for more information about the variables.)

```R
airports_selected_origin <- select(airports, faa, tz_origin = tz, dst_origin = dst)

airports_selected_dest <- select(airports, faa, tz_dest = tz, dst_dest = dst)
````

I then merged the selected columns based on a common key for origin and dest as shown below:

```R
merged_data <- left_join(sampleData, airports_selected_origin, by = c("origin" = "faa"))

merged_data <- left_join(merged_data, airports_selected_dest, by = c("dest" = "faa"))

# View the merged data frame
view(merged_data)
````
#### Conclusion
I found that flights between airports that are in different timezones have `air_time_calc1` that is less than `air_time` (negative `air_time_diff`). So it is possible that the three reasons have something to do with `air_time` not being equal to `arr_time - dep_time`
