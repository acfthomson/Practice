# Python Pandas Exercise
## From [PYnative](https://pynative.com/python-pandas-exercise/)
### Practice working with DataFrames, data selection, groupby(), series, sorting, searching, and statistics

## Resources:
- [Automobile_data.csv](Resources/Automobile_data.csv)
- Jupyter Notebook
    - Python v.3.7.x
        - Dependencies:
            - Pandas
            - Numpy
            
The CSV was first examined by looking at the first and last five rows of the CSV.  The CSV contained columns for company, body-style, wheel-base, length, engine-type, num-of-cylinders, horsepower, average-mileage, and price.

The data needed to be cleaned because some of the values in the 'price' column were missing.  This was done with the following code:
``` python
auto_data_df.loc[(auto_data_df["price"] == "")] = np.nan
```
This code is telling the auto_data_df to locate the 'price' column and anything that is equal to "" (blank) should be set to NaN (not a number).

The max() function was used on auto_data_df to find the most expensive company and price:
```python
most_expensive = auto_data_df[['company', 'price']][auto_data_df.price == auto_data_df['price'].max()]
```
[![most-expensive.png](https://i.postimg.cc/zfxcZfby/most-expensive.png)](https://postimg.cc/Y4m3QMx7)

In order to find all Toyota vehicle details, a new variable 'toyota_details' was created by telling the auto_data_df to locate the 'company' column and anything that is equal to 'toyota'.
```python
toyota_details = auto_data_df.loc[auto_data_df['company'] == 'toyota']
```
[![toyota-details.png](https://i.postimg.cc/QxvYhPdq/toyota-details.png)](https://postimg.cc/MvbmY9Rc)

In order to find the total number of cars per company in this data set, value_counts() was used:
```python
car_count = auto_data_df['company'].value_counts()
```
[![car-count.png](https://i.postimg.cc/mr1HRXh7/car-count.png)](https://postimg.cc/McxTmY7G)

The exercise asked for each company's most expensive car. A variable named 'car_mfg' was created by using the groupby() method on auto_data_df and grouping by 'company'.  The a new variable named 'company_highest_df' was created by finding the highest (max()) price for each company.
```python
car_mfg = auto_data_df.groupby('company')
company_highest_df = car_mfg['company','price'].max()
```
[![company-highest.png](https://i.postimg.cc/6QCpYDyb/company-highest.png)](https://postimg.cc/Jy48hY3j)

The average miles for each car company in auto_data_df was found by using mean() on car_mfg:
```python
average_miles = car_mfg['company', 'average-mileage'].mean()
```
[![average-miles.png](https://i.postimg.cc/Yqj2J4vW/average-miles.png)](https://postimg.cc/ZCthN5Fb)

The top 5 most expensive cars were found by sorting on 'price':
```python
top_5_most_expensive = auto_data_df.sort_values(["price"], ascending = False)
```
[![top-5-most-expensive.png](https://i.postimg.cc/76mDRDD9/top-5-most-expensive.png)](https://postimg.cc/Vrr3SxJ0)

Two new dataframes were created from two provided dictionaries.  The exercise asked to concatonate those two new dataframes and create a key for each dataframe.  Dataframes were created using 'pd.DataFrame.from_dict()' and then both dataframes were combined using 'pd.concat([df1, df2], keys=['x', 'y']).
```python
GermanCars = {'Company': ['Ford', 'Mercedes', 'BMV', 'Audi'], 'Price': [23845, 171995, 135925 , 71400]}
german_cars_df = pd.DataFrame.from_dict(GermanCars)

japaneseCars = {'Company': ['Toyota', 'Honda', 'Nissan', 'Mitsubishi '], 'Price': [29995, 23600, 61500 , 58900]}
japanese_cars_df = pd.DataFrame.from_dict(japaneseCars)

foreign_cars_df = pd.concat([german_cars_df, japanese_cars_df], keys=['Germany', 'Japan'])
```
[![pd-concat.png](https://i.postimg.cc/bwkPh1ps/pd-concat.png)](https://postimg.cc/w1qZ5ytp)

Lastly, the exercise asked to create two more dataframes with provided dictionaries and then merge the dataframes.  This was done using 'pd.merge(df1, df2, on=['column'].
```python
Car_Price = {'Company': ['Toyota', 'Honda', 'BMV', 'Audi'], 'Price': [23845, 17995, 135925 , 71400]}
car_price_df = pd.DataFrame.from_dict(Car_Price)

car_Horsepower = {'Company': ['Toyota', 'Honda', 'BMV', 'Audi'], 'horsepower': [141, 80, 182 , 160]}
car_Horsepower_df = pd.DataFrame.from_dict(car_Horsepower)

new_auto = pd.merge(car_price_df, car_Horsepower_df, on=['Company'])
```
[![pd-merge.png](https://i.postimg.cc/0jT4WH6Z/pd-merge.png)](https://postimg.cc/LgVvhD3Z)
