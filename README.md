# Analyzing-and-Forecasting-Consumer-Card-Spending-Trends-in-Bank-of-Ireland-2015-2023
## 📌 Problem Statement
This project aims to analyze monthly consumer card spending patterns in Ireland using Bank of Ireland transaction data from 2015 to 2023. The goal is to uncover trends across Debit and Credit Cards, as well as different transaction types including POS (Point-of-Sale), ATM, and E-commerce. Additionally, the project includes building a time series forecasting model to predict future spending behaviors. These insights can drive strategic decisions in banking, digital product development, and risk management.
## 🎯 Objectives:
•📊 Explore and visualize long-term monthly card usage trends across different card types •🔍 Compare spending behavior between debit and credit cards, and across transaction types (POS, ATM, E-commerce) •🔮 Build a forecasting model to predict future consumer card spending patterns •📈 Support data-driven decision-making through clear visual storytelling and actionable insights
## Importing Libraries & Loading Data
Begin the analysis, we imported the required libraries for data manipulation, visualization, and time series forecasting. These tools provide powerful capabilities for exploratory data analysis (EDA), trend identification, and predictive modeling.
## Data Cleaning and Preparation
This document describes the steps taken to clean and prepare the dataset containing credit card transaction statistics from Bank of Ireland (2015–2023) for further analysis.
## Dropping Unnecessary Columns
The original dataset contains several columns that are not needed for the analysis. These include identifiers and metadata columns such as:
_id
Category
Sector
Sub-sector
ObservationType
Observation Scale
These columns are dropped to simplify the dataset.
## Verifying the 'Description' Column
o ensure the dataset contains the expected transaction and spending categories, we examine the unique values in the Description column:
## Creating Simplified Labels for Description Categories
The Description column in the dataset contains long and detailed category names, which can be verbose and harder to use in visualizations or analysis. To improve clarity and usability, we created a mapping dictionary that assigns each unique description a simplified and standardized label.
## Step 1: View All Unique Descriptions
We first examined all unique entries in the Description column:
## Verifying Label Mapping Coverage
After applying the description_map dictionary to generate the new Label column, we ran a validation step to ensure all entries in the Description column were successfully mapped.
## Step: Identify Unmapped Descriptions
We filtered the dataset to find any rows where the Label remained NaN after mapping:
## Final Check: Listing Unmapped Descriptions
To ensure completeness, we printed the unique Description values that were not mapped to a Label. This was done using:

## Label Distribution Overview
After mapping the Description column to a simplified Label using our description_map, we examined how many rows correspond to each label:

# 🧪 Exploratory Data Analysis (EDA)

## 📌 Spending Trends Over Time
To understand the temporal dynamics of credit and debit card usage in Ireland (2015–2023), we analyzed spending trends by different categories.
## 🔍 Objective
Identify the top spending categories and observe how their values have evolved over time.
## 📊 Methodology
Group by Label: We calculated the average transaction value (AmountEUR) for each Label across the full period.
Top 10 Labels: We selected the top 10 labels with the highest average spending.
Line Plot: Plotted these categories to visualize temporal spending trends.

## 💳 Focused Trend: Debit vs Credit Card Spending
## 🔍 Objective
To compare how debit and credit card spending patterns have evolved over time from 2015 to 2023.
## 📊 Methodology
We filtered the dataset to include only:
Total_Debit: Total new spending on debit cards
Total_Credit: Total new spending on credit cards
We then visualized their monthly spending trends using a line plot.

## 🏧 POS vs ATM Transactions (Debit Cards)
## 🎯 Objective
To analyze the shift in consumer preference between cash withdrawals (ATM) and direct purchases (POS) using debit cards over time.
## 🛠️ Methodology
Filtered the dataset to include only entries labeled 'ATM' and 'POS'.
Visualized the monthly transaction values in euros (AmountEUR) over the 2015–2023 period.
Used a line plot to clearly illustrate the trend comparison.

## E-Commerce Spending Growth Over Time
## Objective
To visualize the trend of E-Commerce spending in Ireland over time, focusing on overall E-Commerce transactions as well as those specifically made using debit cards.
## Methodology
Filter the dataset to include only records labeled as:
'E-Commerce_All' — total E-Commerce spending across all card types.
'E-Commerce_Debit' — E-Commerce spending using debit cards.
Use a line plot to show how spending amounts have evolved monthly from 2015 to 2023.

## Spending Distribution by Label
## Objective
To analyze and visualize the total spending amounts aggregated by each spending category (Label) from 2015 to 2023.
## Methodology
Group the cleaned dataset by the Label column.
Sum the AmountEUR for each label to get the total spending per category over the entire period.
Sort the labels by total spending in descending order.
Plot the results as a bar chart to clearly compare total spending across categories.

## Seasonality Check: Average Monthly Spending Patterns
## Objective
To analyze and visualize the seasonality in spending by examining the average monthly spending amounts for the top 8 spending categories (Label). This helps identify recurring monthly patterns or seasonal trends in consumer expenditure.
## Methodology
## Extract Month Information
Add a Month column derived from the Date column to capture the month component of each transaction.
## Calculate Average Monthly Spending
Group data by Month and Label to compute the average spending amount (AmountEUR) per month for each spending category.
## Select Top Categories
Identify the top 8 categories based on overall average spending across all months to focus the analysis on the most significant segments.
## Prepare Month Labels
Convert numeric months to abbreviated month names (e.g., Jan, Feb) for readability and set the correct chronological order for plotting.
Plotting
Use a line plot to show average monthly spending trends for each top category, with markers on data points for clarity.

## Preparing Data for Time Series Forecasting
In this step, we filter and format the data to prepare it for time series forecasting models such as Prophet or SARIMAX.

## Visualizing Total Spending Over Time
This code plots the total spending across all cards over the entire time period to observe overall trends and patterns.

## Seasonal Decomposition of Total Spending Time Series
This code performs a seasonal decomposition on the total spending data to break it down into its underlying components: trend, seasonality, and residuals.

## First-Order Differencing of Time Series
This code applies first-order differencing to the total spending time series to help achieve stationarity, which is often required for time series modeling.

## Stationarity Check Using Augmented Dickey-Fuller (ADF) Test on Differenced Series
This code performs the ADF test on the first-order differenced time series to statistically verify if the series is now stationary.

## SARIMAX Model Setup and Fitting
This code fits a Seasonal ARIMA (SARIMAX) model to the time series data for forecasting purposes.

## Forecasting Future Values with SARIMAX and Visualization
This code generates a 12-step (12 months) forecast using the previously fitted SARIMAX model and visualizes the forecast alongside historical data.

## Outcome
The code analyzed Bank of Ireland card spending data (2015–2023, 9801 rows) to uncover trends and forecast future spending. It cleaned the dataset by dropping unnecessary columns, renaming fields (Reporting date → Date, Value → AmountK), scaling to AmountEUR, and mapping 38 Series Description values to simplified labels (e.g., Total_All, Sectoral_Debit). EDA revealed: debit cards (Total_Debit, 3B–6B) dominate credit cards (Total_Credit, ~0.8B–1.5B); POS transactions (1.5B–2.5B) surpass ATM (0.6B–1.5B); E-commerce (E-Commerce_All) shows strong growth; and spending peaks in Nov–Dec. Seasonality analysis confirmed holiday-driven spikes. The SARIMAX model forecast Total_All spending for Apr 2023–Mar 2024, predicting ~5.05B–6.00B monthly, peaking in Dec 2023 (6.0B). The forecast plot showed historical data (2015–2023), a red forecast line, and pink confidence intervals (±0.3B to ±1.0B). The model fit well (AIC ~2479, no residual autocorrelation). Negative values (min -1.1M) and Number Units labels may skew EDA.
