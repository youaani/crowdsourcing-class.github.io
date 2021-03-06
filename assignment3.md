---
layout: default
img: python
caption: Hello world!
title: Homework 3 | Python Bootcamp
active_tab: homework
---


<div class="alert alert-info">
  This assignment is due before class on Wednesday, September 17.  No teams for this assignment, please do it on your own.</div>
<div class="alert alert-info" markdown="span">
Links to tutorials and other Python resources are posted on the [resources page](resources.html).</div>


Python Bootcamp <span class="text-muted">: Assignment 3</span> 
=============================================================
This week we will start writing some code! This assignment is designed to be a crash-course to get you up to speed on the level of Python you will need to know in order to do the remainder of the assignments. For those of you that already know Python, great. You can skip to section 4. For those that do not, its easiest to learn by doing, so please start early so we can help you get on board. You want to spend the semester focusing on the crowdsourcing and machine learning, not the indenting and semicoloning. 
The only deliverable for this assignment will be your script, bootcamp.py. Running your script should print the answers to each of the questions in part 4 of the tutorial, separated by a single blank line. You will submit your code via turnin on the eniac machines. If you have not used turnin before, you can follow the instructions [here](https://alliance.seas.upenn.edu/~cis520/wiki/index.php?n=Resources.HomeworkSubmission). 

Your turnin command will look like this

<pre><code>$ turnin -c nets213 -p python-bootcamp -v bootcamp.py</code></pre>

You do not need to turn in anything for the first 3 sections, but you should read to read through them and walk through the exercises so that you can let us know if you are having trouble.

###1. The basics: variables and data structures

Python has the basic variable types you are used to: strings, ints, floats. Unlike Java and many other languages, variables are not type-checked. You simply declare a variable by assigning a value to it. Later, you can reassign a different type to that same variable and Python couldn't care less.

Open up the python interpreter and play with variable assignment and reassignment:

<pre><code>$ python
# You can comment with pound sign
"""
Or with triple quotes
"""
>>> x = 2
>>> x
2
>>> y = "hello world"
>>> y
'hello world'
>>> x = y # Notice the lack of whining about "incompatible types"...
>>> x
'hello world'
</code></pre>

This also means that you can mix variable types within a data structure. There is no need to specify that L is a list of ints or that M is a map from strings to floats.

Lists are declared with square brackets and indexed using square bracket notation. They can also be treated as stacks, if you are into that sort of thing. 

Create a list of ints. Then, in order to drive those Scala people insane, start appending strings to it. Play with indexing and slicing. In Python, you can use the colon notation to pull out slices of a list. E.g. lst[i:j] will give you a new list which includes the ith through the (j-1)th elements of lst.

<pre><code>>>> l = [1, 2, 3]
>>> for elem in l: #We'll talk about loops more in a bit
...	print elem 
... 
1
2
3
>>> l.append("i am a string. mwahahaha.") 
>>> for elem in l: 
...	print elem 
... 
1
2
3
i am a string. mwahahaha.
>>> l[2]
3
>>> l[1:3]
[2, 3]
>>> l += ['here is more stuff', 6, [2,3,4], 5*1367] 
>>> print l
[1, 2, 3, 'i am a string. mwahahaha.', 'here is more stuff', 6, [2, 3, 4], 6835]
>>> l.pop() 
6835
</code></pre>

Dictionaries (or maps or associative arrays) are probably the favorite data structure of Python. They are a simple key/value store, again without any restrictions on which data types are the keys or values. You can declare dictionaries with curly braces and associate or retrieve keys and values using square bracket notation.

<pre><code>>>> d = {"give me an A!" : "B", "give me a P!" : 7, "give me a Q!" : "no."}
>>> d["give me a P!"]
7
>>> d[14] = 12
>>> d
{'give me a Q!': 'no.', 'give me an A!': 'B', 14: 12, 'give me a P!': 7} # the new k/v pair was added to d
</code></pre>

As you can imagine, the lack of type-checking makes it very easy to write bad Python code. I would advise against doing so. But it is your call, some people like the thrill of nondeterministic runtime errors and such. Don't let me cramp your style.

###2. Control structures and functions

Python makes it easy to write bad code. But it makes it _very_ hard to write ugly code. So chalk one up for superficiality. Python uses whitespace to denote control structures, like loops and if/else blocks. By convention, you should use four spaces for each level of indentation. (I use tabs because I am lazy and like to save the key strokes. I was told over the summer that this is the mark of a novice, and no one of any merit uses tabs. I just hung my head in shame. So use spaces.)

<pre><code>>>> print l
[1, 2, 3, 'here is more stuff', 6, [2, 3, 4]]
# Here is a for loop. 
>>> for elem in l:
...     print elem
... 
1
2
3
here is more stuff
6
[2, 3, 4]
# Here is a while loop
>>> i = 0
>>> while i < 5 : 
...     if i % 2 == 0 : 
...             print "even"
...     else : 
...             print "odd"
...     i += 1
... 
even
odd
even
odd
even
"""
No types are required for parameters, so commenting is SO important. So important.
Returns the idx element of a list

lst - the list 
idx - the integer index of the element to return
"""
>>> def get_list_element(lst, idx) : 
...     return lst[idx]
... 
>>> get_list_element(l, 4)
6
</code></pre>

###3. File IO

You can open, read, and write files using the aptly-named open(), read(), and write() commands. read() returns the entire contents of the file as a string. readlines() will split on the newline character and return the lines as a list, which is generally nicer for allowing you to iterate line-by-line. I won't go through an example here, but I highly recommend playing with the [csv module](https://docs.python.org/2/library/csv.html), which is incredibly useful and we will likely use regularly throughout the semester. 

<pre><code>>>> file = open('test.txt', 'w')
>>> for s in ['line1', 'line2', 'line3', 'line4'] : 
...     file.write(s+'\n')
... 
>>> file.close()
>>> contents = open('test.txt').read()
>>> contents
'line1\nline2\nline3\nline4\n'
>>> contents = open('test.txt').readlines()
>>> contents
['line1\n', 'line2\n', 'line3\n', 'line4\n']
</code></pre>

###4. Text processing in Python

For this part, you will need to submit your code to answer the following questions. 
 
We will be playing with a small but oh so wonderful data set of wine reviews! You can download the data [here](assignments/downloads/python-bootcamp/data.tgz). You can unpack it as follows, and should see two files:

<pre><code>$ tar -xzvf data.tgz 
x data/
x data/stopwords.txt
x data/wine.txt
$ ls data
stopwords.txt	wine.txt
</code></pre>

wine.txt is in the format of one review per line, followed but a star rating between 1 and 5 (except for 3 reviews, where the review decided to go rogue and give 6 stars. Pft.) The text of the review and the star rating are separated by a single tab character. There is also a file called stopwords.txt. You will use this in question 6.

Write a python script that answers each of the following questions and prints the answer to standard output. Since this is a tutorial, there are no secrets: your script should produce [this output](assignments/downloads/python-bootcamp/bootcamp-key.txt) when you are done. I will compare the output of your script directly to this answer key, so start early and come ask for help if you get stuck! I highly recommend looking into the functions available in the [python string module](https://docs.python.org/2/library/string.html).

1. What is the distribution over star ratings?
2. What are the 10 most common words used across all of the reviews, and how many times is each used?
3. How many times does the word 'a' appear?
4. How many times does the word 'fruit' appear?
5. How many times does the word 'mineral' appear?
6. Common words (like 'a') are not as interesting as uncommon words (like 'mineral'). In natural language processing, we call these common words "stop words" and often remove them before we process text. stopwords.txt gives you a list of some very common words. Remove these stopwords from your reviews. Also, try converting all the words to lower case (since we probably don't want to count 'fruit' and 'Fruit' as two different words). Now what are the 10 most common words across all of the reviews, and how many times is each used?
7. You should continue to use the preprocessed reviews for the following questions (lower-cased, no stopwords).  What are the 10 most used words among the 5 star reviews, and how many times is each used? 
8. What are the 10 most used words among the 1 star reviews, and how many times is each used? 
9. Gather two sets of reviews: 1) Those that use the word "red" and 2) those that use the word "white". What are the 10 most frequent words in the "red" reviews which do NOT appear in the "white" reviews?
10. What are the 10 most frequent words in the "white" reviews which do NOT appear in the "red" reviews?

Thats it! Again, you can compare your answers against [our key](assignments/downloads/python-bootcamp/bootcamp-key.txt) to see if you have done things correctly. 

Your code is due <b>Wednesday, September 17</b>. Please submit it via [turnin](https://alliance.seas.upenn.edu/~cis520/wiki/index.php?n=Resources.HomeworkSubmission) from the eniac machines. 
