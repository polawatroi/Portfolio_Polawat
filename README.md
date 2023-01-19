# Portfolio_Polawat
This repasitory was created to demonstrate Polwat Roi-ampaeng's data manipulation skills.

About the company
Nearly New Nautical is a website that allows users to advertise their used boats for sale.

Business Goal
Increasing the number of readers by 75% this year.

Business Task
Understand the boats with more views :

Are they expensive?
What do they have in common?
About the dataset
Column Name: Details
Price : ~ Character, boat price listed in different currencies (e.g. EUR, Â£, CHF etc.) on the website
Boat Type: ~ Character, type of the boat
Manufacturer: ~ Character, manufacturer of the boat
Type: ~ Character, condition of the boat and engine type(e.g. Diesel, Unleaded, etc.)
Year Built: ~ Numeric, year of the boat built
Length: ~ Numeric, length in meter of the boat
Width: ~ Numeric, width in meter of the boat
Material: ~ Character, material of the boat (e.g. GRP, PVC, etc.)
Location: ~ Character, location of the boat is listed
Number of views last 7 days: ~Numeric, number of the views of the list last 7 days
# import libraries
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import statsmodels as sm
# import dataset
df = pd.read_csv('boat_data.csv')
df.head()
Price	Boat Type	Manufacturer	Type	Year Built	Length	Width	Material	Location	Number of views last 7 days
0	CHF 3337	Motor Yacht	Rigiflex power boats	new boat from stock	2017	4.00	1.90	NaN	Switzerland	226
1	EUR 3490	Center console boat	Terhi power boats	new boat from stock	2020	4.00	1.50	Thermoplastic	Germany	75
2	CHF 3770	Sport Boat	Marine power boats	new boat from stock	0	3.69	1.42	Aluminium	Switzerland	124
3	DKK 25900	Sport Boat	Pioner power boats	new boat from stock	2020	3.00	1.00	NaN	Denmark	64
4	EUR 3399	Fishing Boat	Linder power boats	new boat from stock	2019	3.55	1.46	Aluminium	Germany	58
# check out the) data info
print(df.describe())
print(df.shape)
        Year Built       Length        Width  Number of views last 7 days
count  9888.000000  9879.000000  9832.000000                  9888.000000
mean   1893.192860    11.570017     3.520124                   149.160801
std     460.201582     6.002820     1.220534                   151.819752
min       0.000000     1.040000     0.010000                    13.000000
25%    1996.000000     7.470000     2.540000                    70.000000
50%    2007.000000    10.280000     3.330000                   108.000000
75%    2017.000000    13.930000     4.250000                   172.000000
max    2021.000000   100.000000    25.160000                  3263.000000
(9888, 10)
print(df.info())
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 9888 entries, 0 to 9887
Data columns (total 10 columns):
 #   Column                       Non-Null Count  Dtype  
---  ------                       --------------  -----  
 0   Price                        9888 non-null   object 
 1   Boat Type                    9888 non-null   object 
 2   Manufacturer                 8550 non-null   object 
 3   Type                         9882 non-null   object 
 4   Year Built                   9888 non-null   int64  
 5   Length                       9879 non-null   float64
 6   Width                        9832 non-null   float64
 7   Material                     8139 non-null   object 
 8   Location                     9852 non-null   object 
 9   Number of views last 7 days  9888 non-null   int64  
dtypes: float64(2), int64(2), object(6)
memory usage: 772.6+ KB
None
Data Cleaning
# standardize the column name
df = df.rename(columns = str.lower)
df.rename(columns = {'number of views last 7 days' : 'number_of_views_last_7_days', 'year built' : 'year_built'}, inplace = True)
df.columns
Index(['price', 'boat type', 'manufacturer', 'type', 'year_built', 'length',
       'width', 'material', 'location', 'number_of_views_last_7_days'],
      dtype='object')
# removing duplicate enteries
df.drop_duplicates(inplace = True)
# check how many duplicates were removed
no_rows = df.shape
print(no_rows[0])
9888
There are no duplicates

# find missing value
df.isnull().any()
price                          False
boat type                      False
manufacturer                    True
type                            True
year_built                     False
length                          True
width                           True
material                        True
location                        True
number_of_views_last_7_days    False
dtype: bool
There are missing values in the following columns:

manufacturer
type
length
width
material
location
