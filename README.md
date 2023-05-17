# r4da-journey
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

While working with the select() function, I learned how to choose specific variables from the flights data frame:

I selected only the destination column by using the `select()` function with the dest variable.

To extract a range of variables, I utilized the `select()` function with the range specified using the : operator.

Excluding specific variables from the selection was achieved by using the -(variable_name) notation within the `select()` function.

By employing helper functions like `contains()`, `starts_with()`, and `ends_with()`, I could select variables based on specific patterns in their names.

I also discovered the `rename()` function (a variation of `select()`, which allowed me to rename variables within the flights data frame.

I also conducted some exercises to practice different selection scenarios using `select()`:

I brainstormed multiple ways to select the `dep_time`, `dep_delay`, `arr_time`, and `arr_delay` variables from the flights data frame.

I explored the behavior of including the same variable multiple times in a `select()` call.

I learned about the `all_of()` and `any_of()` functions, which proved helpful when combined with a vector of variable names for selection.

I also experimented with the case sensitivity of select helpers and learned how to change the default behavior using the `ignore.case` argument within the helper functions.











