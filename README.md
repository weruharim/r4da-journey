# r4da-journey
My journey of learning R For Data Analysis

## Data Visualisation Using R

This documentation provides examples that I used to learn data visualization techniques in R. The code snippets and explanations below demonstrate how I created various plot types and customization options.

### Prerequisites

Before running the code, I made sure I have the `tidyverse` package installed. I installed it using the following command in R:

```R
install.packages("tidyverse")

### Code Examples
### Scatter Plot

To create a scatter plot, you can use the geom_point() function from the ggplot2 package. The example below plots the displ (displacement) on the x-axis and hwy (highway miles per gallon) on the y-axis.
