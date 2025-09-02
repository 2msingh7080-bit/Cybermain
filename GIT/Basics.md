2025-08-27 07:57

Status:

Tags:

# Basics



Strings 
##  Strings 
Working with Textual Data -Strings 

- data type implementation as string 
	- so variable initialization is not required in python 
		- ``int x = dog ❌``
		- ``x = dog ✅ in python  ``
	- all variables are in small letters
- ``_`` is used for variable with similar name  ''
	- ``name ``
	- ``name_city ``
	- no capital word is  used 
- diffrence b/w  ``' and ''``
- single '  in string
	- ``'may's house'``
		- it thinks ``may's`` is the  end of line not house 
	- `` may\'s house'``
		- it means it ``\'s  is not end of line `` 
- double ``''`` in string
	- ``''may's home''``
		- it works fine with ``''`` 
		- and it even woks same as opposite ``'may"s I know it"s'``
- multi line sting 
	- we use three ``''or'``
		- `` may''s may's may''s `` it works fine 
	- same goes with ``''or'``
- len()
	- to know length of string we use len()
	- ``Print(len((message))``
### Slicing Lists and Strings
- to print charter of string using ``[]``
	- ``Print(message[0])``
- index of list or array ``[]``
	- starts with ``0 and ends with len-1``
- to print charters from string 
	- ``Print(message[0:5])`` 
	- that mean print from 0 till 4 or include 0 til 4 exclude 5  
- to print charters from string from start or end 
	- ``Print(message[:5])`` print from starting  till 5
	- ``Print(message[3:])`` print from 3 till end 

- diffrecne b/w function and method 

### methods  of string 
- lower() method 
	- if  we want to print 
		- `` print("HELLO WORLD") as lower case 
	- we use method called lower()
		- ``print(massage.lower())
	- if want to print as upper case 
		- ``print(massage.upper())

- count() Method  
	- if  we want to count charters as argument in sting 
		- ``print(message.count('l'))``
		-  ``print(word.count('HELLO'))`` ``or word 

- find() method 
	- if  we want to find charters as argument in sting 
		- ``print(word.find('W'))`` 
			- output: ``6``
		- if sting does not 
			- exist it prints ``-1``

- replace() method 
	- to replace sting we need two argument
		- one which to be replaced 
		- one which to be replaced with 
```python
word = "HELLO WORD" 
word = word.replace('HELLO','hello') #  same  variable
word_new = word.replace('HELLO','hello') # or with new variable  
print(word)
```
- strip() method 
	- it removes extra spaces
	-  it remove spacses at stating and ending of string 
```python 
word = "  may be one  "
print(word.strip()) # it remove spacses at stating and ending of string 
 
```
-  split() method 
	- it divides multiple strings 

```python 
text = "may   be   one" 
words = text.split() # splits by whitespace by default print(words) # Output: ['may', 'be', 'one']
```
- joint() method 
	- it joins multiple strings

```python 
words = ['may', 'be', 'one']
result = ' '.join(words)  # joins list elements with a space between
print(result)  # Output: "may be one" 
```
- using spilt() and joint() methods
	- example 
```python
word = '  may   be      one  '
clean_word = ' '.join(word.split())
print(clean_word)
#output  = may be one 
```

### concatenating strings or combining 
 -   example 

```python 
greeting = 'Hello'
name = 'don'
message = greeting + name # it combins but without space 
message = greeting + ', ' + name # does work but it makes diffcult to track
print(message)
```
- string formatting 
	- using palce holers ``{}``
```python 
message = '{}, {}. welcome!'.format(greeting,name)
print(message)
```
- f-strings 
	- it directly uses  the place holder
```python 
message = f'{greeting}, {name.upper()}. welcome!' # we can  also use string method in it 
print(message)
 ```

- to view method, attributes that are available for string or string method

```python 
print(dir(name)) #it  will show variable's  method, attributes that are there
print(help(str)) #it shows what methods do and its attributes
print(help(str.lower)) #it shows what it does and attributes for lower
```


| functions name | use case                 | example                   |
| -------------- | ------------------------ | ------------------------- |
| print()        | prints                   | ``print("llm is  new ")`` |
| len()          | count charters in string | ``Print(len((message))``  |

 



### References
