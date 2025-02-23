# Zomato-Data-Analysis
Zomato Data Analysis
This repository contains a Python script for analyzing Zomato restaurant data. The script performs various data cleaning, visualization, and analysis tasks to gain insights into the dataset.

Original Source
The original file is located at:
https://colab.research.google.com/drive/1WlRcejJy_xhMrWgNIPxcgXCcFxsTI6Hr?usp=sharing

Dataset
The dataset used in this analysis is Zomato data.csv. It contains information about restaurants listed on Zomato, including ratings, votes, online order availability, cost for two people, and more.

Libraries Used
Pandas: For data manipulation and analysis.

NumPy: For numerical operations.

Matplotlib: For creating static visualizations.

Seaborn: For enhanced data visualization.

Script Overview
1. Data Loading and Initial Inspection
python
Copy
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

dataframe = pd.read_csv("Zomato data .csv")
print(dataframe.head())
2. Data Cleaning
The rate column is cleaned to extract numerical ratings:

python
Copy
def handleRate(value):
    value = str(value).split('/')
    value = value[0]
    return float(value)

dataframe['rate'] = dataframe['rate'].apply(handleRate)
print(dataframe.head())
3. Data Information
Basic information about the dataset:

python
Copy
dataframe.info()
4. Visualizations
Countplot of Restaurant Types:

python
Copy
sns.countplot(x=dataframe['listed_in(type)'])
plt.xlabel("Type of restaurant")
Line Plot of Votes by Restaurant Type:

python
Copy
grouped_data = dataframe.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})
plt.plot(result, c='green', marker='o')
plt.xlabel('Type of restaurant', c='red', size=20)
plt.ylabel('Votes', c='red', size=20)
Restaurant with Maximum Votes:

python
Copy
max_votes = dataframe['votes'].max()
restaurant_with_max_votes = dataframe.loc[dataframe['votes'] == max_votes, 'name']
print('Restaurant(s) with the maximum votes:')
print(restaurant_with_max_votes)
Countplot of Online Orders:

python
Copy
sns.countplot(x=dataframe['online_order'])
Histogram of Ratings Distribution:

python
Copy
plt.hist(dataframe['rate'], bins=5)
plt.title('Ratings Distribution')
plt.show()
Countplot of Approximate Cost for Two People:

python
Copy
couple_data = dataframe['approx_cost(for two people)']
sns.countplot(x=couple_data)
Boxplot of Ratings by Online Order Availability:

python
Copy
plt.figure(figsize=(6,6))
sns.boxplot(x='online_order', y='rate', data=dataframe)
Heatmap of Restaurant Types and Online Orders:

python
Copy
pivot_table = dataframe.pivot_table(index='listed_in(type)', columns='online_order', aggfunc='size', fill_value=0)
sns.heatmap(pivot_table, annot=True, cmap='YlGnBu', fmt='d')
plt.title('Heatmap')
plt.xlabel('Online Order')
plt.ylabel('Listed In (Type)')
plt.show()
How to Run
Clone this repository.

Ensure you have the required libraries installed (pandas, numpy, matplotlib, seaborn).

Place the Zomato data.csv file in the same directory as the script.

Run the script using Python.

Insights
The script provides insights into the distribution of restaurant types, the relationship between online orders and ratings, and the most voted restaurants.

Visualizations help in understanding the data distribution and patterns.

License
This project is open-source and available under the MIT License.
