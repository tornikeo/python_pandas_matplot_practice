# python_pandas_matplot_practice

Learning from the code:
2/17/2022
Habit tracker *


```python
def isMonotonic(array):

  #start with edgecases
  if len(array) <= 2:
    return True

  

  direction = array[1] - array[0]     ### Ex: 4-2 = 2 so we know the direction is increasing. 
                                      ### Ex: 2-4 = -2 so we know the direction is decreasing.
                                      
  for i in range(2, len(array)):      ### usually I start at the first number
                                     # here I'm starting at the 3rd number... 
                                     #b/c we used the first two to determine the direction
                                     
      if direction == 0:             #this tripped me up for a while. Monotic includes flat
         direction = array[i] - array[i-1]
         continue
         
         if breaksDirection(direction, array[i-1], array[i]):
            return False
            
  return True
  
  
  def breaksDirection(direction, previousInt, currentInt):
     difference = currentInt - previousInt 
     if direction > 0:  
        return difference < 0  
     return difference > 0  
     
  #review breadthfirst and depth first. Still working on solution.
  ```
  
  Building better pandas fundamentals. Am still working on this code and will push shortly.
  ```python
  names = ['sumlev', 'region', 'division', 'state', 'name', 'census2010pop', 'estimatebase2010', 'popestimate2010', 'popestimate2011', 'popestimate2012', 'popestimate2013', 'popestimate2014', 'popestimate2015', 'popestimate2016', 'popestimate2017', 'popestimate2018', 'popestimate2019', 'popestimate042020', 'popestimate2020']
  ### Learned that creating a list like this is an easy way to rename columns. I create a list of names, in lowercase, and then pass it into the names (columns) parameter. 
  ###When I take header=0 out, then it keeps the old header AND uses our header. Interesting.

nst = pd.read_csv('/content/drive/MyDrive/Datasets/Independent_projects/DataAnalysisCourseMaterials.zip (Unzipped Files)/DataAnalysis/data/nst-est2020.csv', names=names, header=0)  #header = 0 tells it to ignore the header b/c we're providing our own with names. 
nst.head()
  ```
  
I Finally understand this:
```python
bestsellers['User Rating'].dtype      Simply use 'Look up' for whatever column name you choose and then use chaining!
                                      I used to find this so confusing!
                                      
houses['price'].min()                 #similar to just above. Input the column to get the min for that one column
                                      #Will push these and more soon!
                                      
```

Learning from the code:
2/19/2022
Habit tracker **

```python
houses.sum(numeric_only=True)        #numeric only is useful so that we don't sum the dates, object...

titanic['survived'].sum()            #Tells us that 500 people survived (b/c 0=died and 1=survived                                          #here we're summing this one column
titanic.shape                        #1309 (rows) people. 500 survived
```
```python
houses['price].mean()                ####how to round to 2 decimal spaces in this case?
```

```python
titanic.describe().round(2)
```
What does std mean?
                      -lower std means that the values are tighter together (closer to the average)
                      -higher std means values are more spread out or dispersed

What does the 25th percentile mean?      -The value at which 25% of the values lie below that value
What does the 75th percentile mean?      -The value at which 75% of the values lie below that value and 25% above
                    
```python
titanic.describe(include=['O'])          #the default only includes numeric
                                         #You can do 'all' to include all
                                         #or 'O' to include objects - here we're doing 'O' so...
                                         #it's telling up the most frequent names, gender, age...
                                         #age b/c age has '?' marks in the rows
                                         #you can also do include=['object']
```
When to use square bracket vs dot notations?
use square bracket if the column name has a dot in it - titanic.home.dest gives us an error
                                                      - titanic['home.dest'] works
also use [] if you want to select multiple columns
```python
houses.sum(nuermic_only=True)    #b/c we don't want to sum columns like datetime

houses.nlargest(5, ['price'])
```
```python
netflix.release_year.describe()

```

How can you retrieve both the 'price' and 'bedrooms' columns from houses?
```python
select_multiple_cols = houses[['price', 'bedrooms']]
select_multiple_cols
```
```python
houses[['price', 'bedrooms', 'bathrooms']].describe() #getting stats for these three columns

house_size = ['bedrooms', 'bathrooms', 'sqft_living']          #might be easier to read way to do it 
houses[house_size]  #still nested list
```

How can you use .value_counts() on multiple columns?
```python
houses[['bedrooms', 'bathrooms']].value_counts()
```

What's the default for .plot(). - What does it compare the X with by default?... - the index (which might not be that useful).
You can make the value_counts() the index with:
```python
houses.bedrooms.value_counts().plot()
#A line chart is the default.

How can we change the kind to make it more readable:
```
houses.bedrooms.value_counts().plot(kind='bar')     #We can easily change the kind=... This shows us                                                        that 2-4 bedrooms are the most common
```python
titanic['survived'].value_counts().plot(kind='pie')   #each passanger is either 0 or 1
                                                      #very interesting!
```
the above is for plotting in a Series
In a dataframe you got to specify which data is for the X and which for the y! ###

So for the houses dataset let's rename it df
bedrooms vs bathrooms...which should we associate with x vs y
In general, stuff like time and price go on y
Here bed vs bath we'd prob want to put bedrooms on x b/c they range from 0-30 (higher std) than baths
This usually works best b/c computer screens are wider than they are tall

books_df.plot(x='Name', y='Price', kind='bar');   #put price or time on y whenever you to compare them.

```python
netflix.rating.value_counts().head(8).plot(kind='bar)
```
```python
books_df.sort_values(by=['Price'], ascending=False)  ###the by= is very interesting
```
In plotting, what is barh and when might we use it?
```python
bestsellers['Author'].value_counts().head(10).plot(kind='barh');   ###barh easier to reach in this case - h == horizontal
```

I didn't previously understand what the point of 'Histograms are' that well.
I learned that they are cool b/c they automatically include the value counts, so no need to do .value_counts()
```python
bestsellers['User Rating'].plot(kind='hist');         ###Very useful
```
pandas uses 0, 1, 2 as the default index. You can change it to whatever makes the most sense, for example the date

```python
btc = pd.read_csv('/content/drive/MyDrive/Datasets/Independent_projects/DataAnalysisCourseMaterials.zip (Unzipped Files)/DataAnalysis/data/coin_Bitcoin.csv')
btc.head()   #there's a lot of repetive info here such as Bitcoin, BTC (they're all BTC).

```
Let's just focus on the name, date and high and low prices
```python
btc['High'].plot() #b/c we reset the index, now the Date show up on the bottom instead of the range of                     0 to 2991
```

```python
countries.set_index('Country', inplace=True)  #Taking a quick look at the countries df, likely we'd                                                     want the country to be the index...not 0, 1, 2...
countries                                       so we set_index to Country and save it
```
Notice how many spaces and funky characters there are in the column names such as: (per sq. mi.)
if we were doing something serious with these, we're probably want to rename them to something simplier

set index right in read_csv is the easiest way to do it
```python
df = pd.read_csv('/content/drive/MyDrive/Datasets/Independent_projects/DataAnalysisCourseMaterials.zip (Unzipped Files)/DataAnalysis/data/world-happiness-report-2021.csv', index_col='Country name')
df.head(3)
```

df['Ladder score']   #the general world happiness report score
b/c we set the countries to the index, now it makes more sense (it's no longer just 1, 2, 3...with the score)
```python
df.sort_values('Healthy life expectancy').head(3)  #goes from lowest to highest by default
```
I struggle a little bit to understand lambda. It makes better sense here
```python
titanic.sort_values('name', key=lambda col: col.str.lower()) lambda is a function.
                                                             Here we give it one parameter
                                                             then we tell it what to do with that param
```

Start on .loc...Create a new Readme.

