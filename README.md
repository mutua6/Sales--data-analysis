# Sales--data-analysis
Sales data analysis and visualization using R programming.
# Install required packages (if not already installed)
install.packages(c("tidyverse", "lubridate"))

# Load necessary libraries
library(tidyverse)
library(lubridate)

# Load the dataset
sales_data <- read.csv("sample_sales_data.csv")

# Convert Date column to Date format
sales_data$Date <- as.Date(sales_data$Date)
# View first few rows of the dataset
head(sales_data)

# Check data structure
str(sales_data)

# Summary statistics
summary(sales_data)
# Aggregate total sales per day
daily_sales <- sales_data %>%
  group_by(Date) %>%
  summarise(Total_Sales = sum(Total_Sales))

# Plot sales trend over time
ggplot(daily_sales, aes(x = Date, y = Total_Sales)) +
  geom_line(color = "blue", size = 1) +
  labs(title = "Daily Sales Trend", x = "Date", y = "Total Sales") +
  theme_minimal()
  # Aggregate total sales by product
product_sales <- sales_data %>%
  group_by(Product) %>%
  summarise(Total_Sales = sum(Total_Sales))

# Bar chart for sales by product
ggplot(product_sales, aes(x = reorder(Product, -Total_Sales), y = Total_Sales, fill = Product)) +
  geom_bar(stat = "identity") +
  labs(title = "Total Sales by Product", x = "Product", y = "Total Sales") +
  theme_minimal()
  # Aggregate total sales by region
region_sales <- sales_data %>%
  group_by(Region) %>%
  summarise(Total_Sales = sum(Total_Sales))

# Bar chart for sales by region
ggplot(region_sales, aes(x = reorder(Region, -Total_Sales), y = Total_Sales, fill = Region)) +
  geom_bar(stat = "identity") +
  labs(title = "Total Sales by Region", x = "Region", y = "Total Sales") +
  theme_minimal()
