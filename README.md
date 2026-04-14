# Overview

Welcome to my analysis of the data job market (2023) 

This project pursues two goals:

1) to help me, as a beginner analyst, understand the market of data‑related job openings, identify the most in‑demand roles, and determine the most optimal skill set for a newcomer;

2) to develop my skills in working with Python, especially with pandas.

I am sincerely grateful to [Luke Barousse's Python Course](https://lukebarousse.com/python) for the dataset and the guides that became the foundation of my work.**
(Despite the fact that the data is somewhat outdated (2023), I still believe it reflects long‑term trends in the labor market for data‑related roles and employer requirements.)

# The Questions

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?(Only USA market)
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying) 


# Tools I Used

    **Python** - (pandas,matplotlib,seaborn)
    **Jupyter Notebooks**
    **VS Code** 
    **Git and GitHub**

# Data Clean Up

Each notebook begins with importing the necessary libraries and performing a small amount of data cleaning. The dataframe itself is of high quality and does not require extensive preprocessing for our analysis.
The first thing I do is convert the 'job_posted_date' column to the datetime format.
The second step concerns the 'job_skills' column, which stores data as a string. To fix this, I use a lambda function together with ast.literal_eval, after which the values are converted into a list.

```python
import ast
import pandas as pd
from datasets import load_dataset
import matplotlib.pyplot as plt
import seaborn as sns

# Loading data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

#Data cleanup 
df['job_posted_date'] = pd.to_datetime(df.job_posted_date)
# Converting job_skills column to list
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter  

In my analysis, I apply country‑based filters. In most cases, the data refers to the EU region, but for the salary‑related part of the project I use data from the USA, since it is the most abundant in the dataset.
```python
europe_countries = [
    "Albania", "Andorra", "Austria", "Belgium",
    "Bosnia and Herzegovina", "Bulgaria", "Croatia", "Cyprus",
    "Czech Republic", "Denmark", "Estonia", "Finland", "France",
    "Germany", "Greece", "Hungary", "Iceland", "Ireland",
    "Italy", "Kosovo", "Latvia", "Liechtenstein", "Lithuania",
    "Luxembourg", "Malta", "Moldova", "Monaco", "Montenegro",
    "Netherlands", "North Macedonia", "Norway", "Poland",
    "Portugal", "Romania", "San Marino", "Serbia", "Slovakia",
    "Slovenia", "Spain", "Sweden", "Switzerland", "Ukraine",
    "United Kingdom", "Vatican City"
]
df_eu = df[df['job_country'].isin(europe_countries)]
```
or

```python
df_US = df[(df['job_country'] == 'United States')].dropna(subset=['salary_year_avg'])
```

# The Analysis

First view [EDA Intro](1_EDA_Intro.ipynb)

## Country variety 

The dataset contains more than 700,000 job postings from 160 countries worldwide for the year 2023. A significant share — around 26% — comes from the United States.

[Distribution by country](images/job_post_countries.png)
