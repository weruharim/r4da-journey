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

### Code Examples
### Scatter Plot

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
###Filtering data using `filter()` in R
In my data analysis journey with R, I have learned how to use the `filter()` function to extract specific rows from a dataset based on certain conditions.

To begin, I loaded the necessary libraries, including the `tidyverse` and `nycflights13` packages. I also loaded the flights dataset from the `nycflights13` package to work with. This dataset contains information about flights that department New York in 2013.

To get a better understanding of the dataset, I used the `view()` function to see the entire flights data frame. Additionally, I explored the documentation for the `flights` dataset using the `?flights` command.

To filter the data and extract specific flights, I utilized the `filter()` function. For example, I filtered the flights dataset to extract flights that occurred on January 1st by specifying the conditions `month == 1` and `day == 1`. I stored the filtered data in a new data frame called `jan1`.

To view the `jan1` data frame, I used the `view()` function again. Alternatively, I could print the new data frame by enclosing the assignment in parentheses, like this: `(jan1 <- filter(flights, month == 1, day == 1))`.

Next, I experimented with filtering the flights dataset using comparison operators. I filtered flights with a departure delay of less than or equal to -20 minutes by applying the condition `dep_delay <= -20`. Similarly, I filtered flights with an air time of 60 minutes or more using the condition `air_time >= 60`.

I also explored the use of Boolean operators to filter data based on multiple conditions. For instance, I filtered flights that occurred in October, November, or December and covered a distance of over 1000 miles. I achieved this by combining the conditions `(month %in% c(10, 11, 12))` and `distance > 1000`.

In addition to the examples above, I completed a series of exercises to further practice filtering data using the `filter()` function. These exercises involved filtering flights based on various criteria such as arrival delay, destination, operating airline, departure month, and more. For each exercise, I used the `filter()` function with the corresponding conditions and stored the filtered data in new data frames. To examine the results, I utilized the `view()` function to inspect each filtered data frame.

Throughout my learning process, I also discovered the usefulness of the `between()` function. I utilized this function to filter flights that occurred in the summer months (July, August, and September) and flights that departed between midnight and 6 am.

Lastly, I explored the concept of missing values and filtered flights that had a missing departure time using the `is.na()` function.

By applying the `filter()` function and exploring various conditions and operators, I gained a better understanding of how to extract specific subsets of data from a larger dataset.

Feel free to modify and experiment with the code to further enhance your data analysis skills using the `filter()` function.
















