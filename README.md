# Real-Estate-Data-Collection-and-Cleaning-Project

## objectives
This project is designed to simulate a real-world data science task. You will scrape property data from two real estate websites, clean and integrate the data, engineer features, and frame a predictive modeling challenge based on pricing.


## 	Websites used:
- [Bayut Oman](https://www.bayut.om/en/)
- [OpenSooq Oman](https://om.opensooq.com/en/property)

##  Steps taken in data collection and cleaning:
### This is cleaning for opensooq website
1- df.isnull()

2- df.isnull().sum()

3- df['Location'] = df['Location'].fillna(df['Location'].mode()[0])
   df['Size'] = df['Size'].fillna(df['Size'].median())

4- df.isnull().sum()

5- df.dtypes

6- Extract numeric part (if it's a string with text)
   df['Size'] = df['Size'].astype(str).str.extract(r'(\d+\.?\d*)')
   Convert to float first (to handle decimals safely)
   df['Size'] = pd.to_numeric(df['Size'], errors='coerce')
   Convert to integer
   df['Size'] = df['Size'].astype('Int64')

7- df.dtypes

8- df['Price'] = df['Price'].astype(str).str.extract(r'(\d+\.?\d*)')
   Convert to float first (to handle decimals safely)
   df['Price'] = pd.to_numeric(df['Price'], errors='coerce')
   Convert to integer
   df['Price'] = df['Price'].astype('Int64')

9- df.dtypes

10- Strip whitespace and lowercase text in relevant columns
    df['Title'] = df['Title'].str.strip()
    df['Location'] = df['Location'].str.strip()
    df['Listing_Type'] = df['Listing_Type'].str.strip().str.lower()

11- df.head()

12- Drop duplicates 
    df.drop_duplicates()
     
13- df.isnull().sum()

14- ['Price'] = df['Price'].fillna(df['Price'].median())

15- df.isnull().sum()

16-  savec leaned DataFrame as csv file
     df_opensooq_clean.to_csv("cleaned_opensooq.csv", index=False)

## Feature engineering strategy
In this feature engineering strategy, we created a new metric called price per square meter to better compare property values regardless of size. We then used one-hot encoding to convert categorical variables like property type and city into numerical format, which machine learning models can understand. We also cleaned and converted the price column to ensure it was numeric. To improve data quality, we removed outliers using the IQR method, which filters out extreme values. Finally, we scaled the numerical features using both MinMaxScaler and StandardScaler to normalize values, ensuring all features contribute fairly to model training.
