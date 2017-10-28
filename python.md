# Starting with Python

Python is a very popular programming language used to create many things, from desktop programs to websites.

Fortunately it is included by default on the Raspberry Pi, so we don't have to go to the trouble of installing it.

In this lesson we will look at the language very briefly, and start thinking about some of the things you can do with it.

## Basic Python

We will use Python quite a bit in this course — it is used to control quite a lot of things on the Pi. To start with, we will go through a number of basic features of the language to get you familiar. To achieve this, we will follow the Raspberry Pi Foundation's [Basic Python](https://www.raspberrypi.org/documentation/usage/python/) tutorial. Open this link in a new browser tab now.

### Some teacher's notes

* When the tutorial starts to use indentation, the REPL starts to become annoying. At this point, use a Python file (in the REPL, do File > New File)
* To save a file, do File > Save As... and then choose somewhere memorable to save your file, like the desktop.
* To run your file, in the file window do Run > Run Module

### Simple if else example

Simple:

```
weather = "sunny"

if(weather == "sunny"):
  print("I think I'll go outside and have a picnic")
elif(weather == "rainy"):
  print("I think I'll stay inside and chill")
```

### Example of an import

To use certain Python functionality, you have to import it from code repositories called modules. This is done using the ```import``` keyword.

```
import time

weather = input()

if(weather == "sunny"):
  print("I think I'll go outside and have a picnic")
elif(weather == "rainy"):
  print("I think I'll stay inside and chill")
else:
  print("Let's get some lunch")

time.sleep(2)

print("Right. Glad that's decided!")
```

### Simple len example

```
name = "Chris"
print(len(name))
```

### Function example

```
def greeting():
  name = input()
  print("Hello " + name + "! How are you?")

greeting()
```

### Function example

```
def greeting():
  name = input()
  print("Hello " + name + "! How are you?")
  greeting()

greeting()
```

## Simple random insult program

```
import random

var insults = [
  "Your hair looks like a hedge",
  "Your feet smell of cheese",
  "Your nose could be used to vacuum the floor",
  "Your teeth look like tombstones",
]

def insult_me():
  rand = random.randInt(0,len(insults)-1)
  print(insults[rand])

insult_me()

```

# See also

* (The Python tutorial)[https://docs.python.org/3/tutorial/]
* (Learn Python)[https://www.learnpython.org/]
* (Codecademy Learn Python)[https://www.codecademy.com/learn/learn-python]
