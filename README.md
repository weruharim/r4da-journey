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

## Faceting
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

## Other Plot Types
Here are a few examples of other plot types that I created using R:

### Smooth Chart

To create a smooth chart, use the geom_smooth() function. Here's an example:

```R
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy))
```
### Boxplot

To create a boxplot, use the geom_boxplot() function. Here's an example:

```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_boxplot()
```

### Line Chart
To create a line chart, use the geom_line() function. Here's an example:
```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_line()
```

### Area Chart

To create an area chart, use the geom_area() function. Here's an example:

```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_area()
```
### Histogram

To create a histogram, use the geom_histogram() function. Here's an example:

```R
ggplot(data = mpg, mapping = aes(x = displ)) +
  geom_histogram(binwidth = 1)
```


















