![Python Logo](http://miriamposner.com/classes/dh101f16/wp-content/uploads/sites/5/2016/11/Python_logo.png)
## Table of Contents

1. [**Strings**](#strings)
	- [**Slicing**](#stringslicing) 
2. [**Pandas DataFrames**](#dataframes)
	- [**Working with Indexes**](#indexes) 
3. [**Miscallaneous**](#misc)
	- [**Timing your Script**](#timing) 	


## Strings <a name = "strings"></a>

### Slicing Strings <a name = "stringslicing"></a>

Python strings have a very useful functionality whereby you can "slice" them. That is to say you can easily grab parts of the strings you want. 

To access a single character of a string just use the `[]` brackets and enter the position of the character you want (keep in mind that Python indexes from 0!). 

```python
In [3]: x = "Much Wow!"

In [4]: x[3]
Out[4]: 'h'
```

You can also access a range of characters, but remember that Python will not grab the character at the last index. To do this simply use the `[]` brackets and entering your desired ranging starting from **x** going to **y** seperated by `:`: `[x:y]`

```python
In [5]: x[0:3]
Out[5]: 'Muc'
```

Oops, let's try to get the whole word this time. Note that `h` is at the index 3 but Python won't grab the character at the last index like I mentioned above, so we need to extend our range to 4.

```python
In [5]: x[0:4]
Out[5]: 'Much'
```
If we just wanted to get everything from the beginning of the string up to a certain point there is a simpler way, to do so just indicate endpoint of the range you want with a blank space for the starting point:

```python
In [5]: x[:4]
Out[5]: 'Much'
```
Similary, we can extract the string from some starting point in the middle all the way to the end of the string:

```python
In [7]: x[2:]
Out[7]: 'ch Wow!'
```
Sometimes, we might have really long strings and we want to access things at the end. We don't want to have to count the exact index from the beginning so that we can access part of the string at the end. In these cases we can use negative indexes to start from the back, with `-1` giving the last character in the string. 

```python
In [8]: x = "Mississippi" # uh oh, long string

In [9]: x[-1] # get the last character
Out[9]: 'i'

In [10]: x[-3:-1] # get something from the end
Out[10]: 'pp'

In [11]: x[-4:] # get the back of the string starting from some point
Out[11]: 'ippi'
```

## DataFrames <a name = "dataframes"></a>

### Working with Indexes <a name = "indexes"></a>

Sometimes you might find yourself in a situation where you want to change your indeces. There are a lot of things you can do here but some of the issues I run into the most I've outlined below.

***Making the Index a Column***

Let's say you'd like to make the index you have into a column, say it is storing some important information - this sometimes happens when converting a `dict` into a `dataframe`.

```python
                             year
Mississippi                  1978
Oklahoma                     3056
Wyoming                      1107
Minnesota                   13988
Illinois                    28329
Arkansas                     2501
New Mexico                   2759
Ohio                        19671
Indiana                      6286
```

Doing so is easy. To turn the index into a column use the `df.index` to retrieve the values of the index, and then store them in a column, naming the column whatever you'd like, in this case I am calling it `'index'`.

```python
df['index'] = df.index
```
As you can see, the states that were once the index, now became a column named `'index'`.

```python
     year                       index
0    1978                 Mississippi
1    3056                    Oklahoma
2    1107                     Wyoming
3   13988                   Minnesota
4   28329                    Illinois
5    2501                    Arkansas
6    2759                  New Mexico
7   19671                        Ohio
8    6286                     Indiana
```

***Re-Indexing***

Now maybe your index is messed up and you'd like to change the index so that it marks the observations in order: 0, 1, 2, 3. To do so, once again use `df.index`, but this time we will use the `range()` function to give the endpoint of a range starting from 0 to `1-endpoint`. In this case we want the endpoint to be the number of observations in our dataframe, which we can retrieve with `len(df)`.

```python
df.index = range(len(df))
```

## Miscallaneous <a name = "misc"></a>

For things that don't currently have a home.

### Timing your Program <a name = "timing"></a>

Sometimes, it might be useful or interesting to see how long it takes for your Python script to execute. This can be done with a function from the package `datetime`. We will merely subtract the time the program started from the time it executed it's last line.

```python
from datetime import datetime
startTime = datetime.now()

#here goes your code

#last line
print datetime.now() - startTime
```
