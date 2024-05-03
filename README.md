# MongoDB Yelp Academic Dataset Analysis

Welcome to the MongoDB Yelp Academic Dataset Analysis repository! This project focuses on exploring how various database systems manage semi-structured JSON data, with a particular emphasis on MongoDB, a document-oriented database system. We utilize the Yelp Academic Dataset, which comprises data about businesses, reviews, and users. Note that due to system constraints, the review and user data are truncated to 7500 reviews and 1000 users, respectively, while the full business dataset is utilized.

## Data Files

The project includes the following files in the `data` folder:
- `business.csv`
- `review.csv`
- `yelp_academic_dataset_business.json.zip`
- `yelp_academic_dataset_review.json.zip`
- `yelp_academic_dataset_user.json.zip`

## Setup and Configuration

- **Python Libraries:** This project uses Pymongo, a Python wrapper for MongoDB, to interact with the database.
- **Database Configuration:** We initiate a MongoDB client and define collections for businesses, reviews, and users.

```python
import pandas as pd
import pymongo
from pymongo import TEXT
import numpy as np

myclient = pymongo.MongoClient("mongodb://localhost")
mydb = myclient["yelp"]
business = mydb["business"]
review = mydb["review"]
user = mydb["user"]
```

## Loading Data

We load the JSON datasets into MongoDB collections, handling ZIP files and checking for existing data to avoid duplicates.

```python
import zipfile
import os.path
import json

# Example of loading business data
if business.count_documents({}) == 0:
    print("Loading business collection...")
    with open('data/yelp_academic_dataset_business.json', encoding='utf-8') as f:
        for line in f:
            business.insert_one(json.loads(line))
```

## Query Examples

- **Finding specific business hours:** We write queries to extract specific information, such as business hours for a particular restaurant.
- **Aggregation Pipelines:** We utilize MongoDB's powerful aggregation framework to compute statistics such as the average star rating across businesses and to find the town in each state with the highest average number of stars.

## Analysis

- **Sentiment Analysis:** Identifying negative reviews by searching for specific words and flagging them for avoidance.
- **Data Size Analysis:** Examining the impact of adding or removing fields on the size of the data stored in MongoDB.

## Data Export

We demonstrate how to export data from MongoDB to Pandas DataFrames for further analysis and integration with other data tools.

```python
from pandas import json_normalize

# Convert MongoDB cursor to DataFrame
user_df = json_normalize(user_cursor)
```

## Usage

Feel free to clone this repository to run and modify the analyses. Detailed comments and documentation within the scripts will guide you through the processes.

Thank you for visiting this project!
