# This file contains the answers to the Udacity Two Variable EDA problem set. This problem uses the diamonds data set. 

# Load necessary datasets:
library(dplyr)
library(ggplot2)

# First we need to get the data
data("diamonds")

#Turn diamonds into a table
tbl_df(diamonds)
# The first excerise is to get a scatterplot of price vs. x using ggplot
ggplot(data = diamonds, aes(x = price, y = x))+
  geom_point()

# Save the plot
ggsave('DiamondPlot1.png')

# Next we need to calculate a series of correlation values
cor.test(diamonds$price, diamonds$x)
cor.test(diamonds$price, diamonds$y)
cor.test(diamonds$price, diamonds$z)

# Next we need to create a plot of 
ggplot(data = diamonds, aes(x = price, y = depth))+
  geom_point()

# Save the plot
ggsave('DiamondPlot2.png')

# Next we need to create transparency of a point equal to 1/100 and create breaks every 2 values on the x axis
ggplot(data = diamonds, aes(x = price, y = depth))+
  geom_point(alpha = 1/100)+
  scale_x_continuous(breaks = 326, 18823, 2)

# Save the plot
ggsave('DiamondPlot3.png')

# Next we've got to look at the numeric correlation between price vs. depth
cor.test( diamonds$depth, diamonds$price)

# Next create a scatter plot of price vs. carat, omit the top 1% of price and carat values
# Start with getting the values of 99% of the data
nnp <- quantile(diamonds$price, probs = .99)
nnc <- quantile(diamonds$carat, probs = .99)

# Make the graph
ggplot(data = diamonds, aes(x = carat, y = price)) +
  geom_point() +
  xlim(0, nnc) +
  ylim(0, nnp)

# Next create a variable for volume (as defined by x*y*z) and create a plot of price vs. volume
# Create new value and turn volume to a table
diamonds$volume<- diamonds$x*diamonds$y*diamonds$z

# Create graph
ggplot(data = diamonds, aes(x= volume, y = price)) + 
  geom_point()

# Next find correlation excluding volumes of 0 or greater than 800
# Filter the data
with(subset(diamonds, volume<800), cor.test(price, volume))

       
         
         

