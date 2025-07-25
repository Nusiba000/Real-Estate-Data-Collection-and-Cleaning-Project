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

### This is cleaning for bayut website

1- df.isnull()

2- df.head(60)

3- df.isnull().sum()

4- df.replace('not available', np.nan, inplace=True)

5- df.isnull().sum()

6- fill the missing value
   df.fillna('some default value', inplace=True) 
   
7- df.isnull().sum()

8- df.dtypes

9- df['rooms'] = pd.to_numeric(df['rooms'], errors='coerce')

10- df.dtypes

11- df.head()

12- df['size'].unique()[:20]

13- Remove non-numeric characters(sq, m,)
    df['size'] = df['size'].str.extract('(\d+\.?\d*)') # extracts numeric part as string
    df['size'] = pd.to_numeric(df['size'], errors='coerce') # convert it to float
    
14- df.dtypes

15- Clean the 'price' column
    df['price'] = df['price'].astype(str).str.replace(r'[^\d.]', '', regex=True)
    Convert to float first
    df['price'] = pd.to_numeric(df['price'], errors='coerce')
    Convert to nullable integer
    df['price'] = df['price'].astype('Int64')

16- df.dtypes

17- df['size'].isnull().sum()

18- df.head()

19- convet DataFrame to csv file
    df.to_csv('cleaned_bayut.csv', index=False)


## Feature engineering strategy
In this feature engineering strategy, we created a new metric called price per square meter to better compare property values regardless of size. We then used one-hot encoding to convert categorical variables like property type and city into numerical format, which machine learning models can understand. We also cleaned and converted the price column to ensure it was numeric. To improve data quality, we removed outliers using the IQR method, which filters out extreme values. Finally, we scaled the numerical features using both MinMaxScaler and StandardScaler to normalize values, ensuring all features contribute fairly to model training.
