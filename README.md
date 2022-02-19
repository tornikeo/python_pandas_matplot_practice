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

```
houses.sum(numeric_only=True)        #numeric only is useful so that we don't sum the dates, object...

titanic['survived'].sum()            #Tells us that 500 people survived (b/c 0=died and 1=survived                                          #here we're summing this one column
titanic.shape                        #1309 (rows) people. 500 survived
```
```
houses['price].mean()                ####how to round to 2 decimal spaces in this case?
```

```
titanic.describe().round(2)
```
What does std mean?
                      -lower std means that the values are tighter together (closer to the average)
                      -higher std means values are more spread out or dispersed

What does the 25th percentile mean?      -The value at which 25% of the values lie below that value
What does the 75th percentile mean?      -The value at which 75% of the values lie below that value and 25% above
                    
```
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
```
houses.sum(nuermic_only=True)    #b/c we don't want to sum columns like datetime

houses.nlargest(5, ['price'])
```
```
netflix.release_year.describe()

```

How can you retrieve both the 'price' and 'bedrooms' columns from houses?
```
select_multiple_cols = houses[['price', 'bedrooms']]
select_multiple_cols
```
```
houses[['price', 'bedrooms', 'bathrooms']].describe() #getting stats for these three columns

house_size = ['bedrooms', 'bathrooms', 'sqft_living']          #might be easier to read way to do it 
houses[house_size]  #still nested list
```

How can you use .value_counts() on multiple columns?
```
houses[['bedrooms', 'bathrooms']].value_counts()
```

What's the default for .plot(). - What does it compare the X with by default?... - the index (which might not be that useful).
You can make the value_counts() the index with:
```
houses.bedrooms.value_counts().plot()
