---
layout: python
title: Python
---

## Table of Contents

1. [**Strings**](#strings)
   - [**Basics**](#stringsbasics)
   - [**Built-in-Functions**](#stringfunc)
	- [**Slicing**](#stringslicing)
2. [**Pandas DataFrames**](#dataframes)
	- [**Working with Indexes**](#indexes)
3. [**Miscallaneous**](#misc)
	- [**Timing your Script**](#timing) 	


# Strings <a name = "strings"></a>

### Basics <a name = "stringsbasics"></a>

Strings are an extremely useful and powerful data type in Python. Basically, strings are just a "list" of characters. Although Python does not support a char type its easy to think of them in this way. As you'd expect its pretty straightforward to create a string:

```python
In [1]: x = "this is a string"

In [2]: x
Out[2]: 'this is a string'
```
Like Java, you can add or "concatenate" strings together:

```python
In [3]: x = "Hello"

In [4]: y = "World"

In [5]: z = x + " " + y

In [6]: z
Out[6]: 'Hello World'
```
You can also iterate through strings using a `for` loop:

```python
In [10]: word = "Doge"

In [11]: for letter in word:
    ...:     print(letter)
    ...:     
D
o
g
e
```
It's is also very easy to test for string/substring membership or seeing whether a string you're interested in lies in another string:

```python
In [20]: x = "Is Doge Home?"

In [21]: def knock_knock(x):
    ...:     if "Doge" in x:
    ...:         print("Doge is Home")
    ...:     else:
    ...:         print("Doge isn't home!")
    ...:         

In [22]: knock_knock(x)
Doge is Home
```


### Basic Functions <a name = "stringfunc"></a>

Python has some handy built-in functions for working with strings. Take for instance, the `len` function, which gives us the "length" or number of characters in the string:

```python
In [23]: word = "Doge"

In [24]: len(word)
Out[24]: 4

In [25]: word = "Spaces count"

In [26]: len(word)
Out[26]: 12
```
There is also the `format()` function which is powerful for working with and formatting strings. This function uses `{}` as a placeholder for strings:

```python
In [27]: ordering = "{}, {}, and {}".format("Doge", "Cate", "Duck")

In [28]: print(ordering)
Doge, Cate, and Duck
```
You can also use the ordinal positions of your arguments!

```python
In [29]: ordering = "{1} is first, {2} is second, and {0} is last".format("Cate"
    ...: , "Doge", "Duck")

In [30]: ordering
Out[30]: 'Doge is first, Duck is second, and Cate is last'
```
You can also give your arguments names and use that instead:

```python
In [31]: ordering = "a goes here {a}, b goes here {b}, and c goes all the way ov
    ...: er there ..... {c}".format(a="A", b="B", c="C")

In [32]: ordering
Out[32]: 'a goes here A, b goes here B, and c goes all the way over there ..... C'
```

You can also convert strings to upper and lower case easily with `string.lower()` and `string.upper()`:

```python
In [33]: word = "make me big"

In [34]: word.upper()
Out[34]: 'MAKE ME BIG'

In [35]: word.lower()
Out[35]: 'make me big'
```
Just as we can `split()` strings we can also `join()` them. `join()` interweaves the provided string into the passed in string:

```python
In [36]: word = "hyphenate"

In [37]: "-".join(word)
Out[37]: 'h-y-p-h-e-n-a-t-e'
```
Although that was a trivial example, we can use `join()` in other clever ways:

```python
In [41]: " and ".join(["Doge", "Cate", "Snek"])
Out[41]: 'Doge and Cate and Snek'
```
We can also make simple adjustments to strings using `string.replace()` and passing in a few arguments: `string.replace(replace, replace with)`:

```python
In [42]: sentence = "Cate was evil"

In [43]: sentence.replace("was", "is")
Out[43]: 'Cate is evil'
```

### Slicing Strings <a name = "stringslicing"></a>

Python strings have a very useful functionality whereby you can "slice" them. That is to say you can easily grab parts of the strings you want.

To access a single character of a string just use the `[]` brackets and enter the position of the character you want (keep in mind that Python indexes from 0!).

```python
In [3]: x = "Much Wow!"

In [4]: x[3]
Out[4]: 'h'
```

You can also access a range of characters, but remember that Python will not grab the character at the last index. To do this simply use the `[]` brackets and entering your desired ranging starting from **x** going to **y** separated by `:`: `[x:y]`

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

# DataFrames <a name = "dataframes"></a>

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

# Miscellaneous <a name = "misc"></a>

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
