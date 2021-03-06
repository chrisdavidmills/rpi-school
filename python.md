# Starting with Python

Python is a very popular programming language used to create many things, from desktop programs to websites.

Fortunately it is included by default on the Raspberry Pi, so we don't have to go to the trouble of installing it.

In this lesson we will look at the language very briefly, and start thinking about some of the things you can do with it.

## Basic Python

We will use Python quite a bit in this course — it is used to control quite a lot of things on the Pi. To start with, we will go through a number of basic features of the language to get you familiar. To achieve this, we will follow the Raspberry Pi Foundation's [Basic Python](https://www.raspberrypi.org/documentation/usage/python/) tutorial. Open this link in a new browser tab now.

We can start up Python by choosing Programming > Python 3 in the main Pi menu. This opens up simple program called a REPL (Read–Eval–Print Loop), which allows you to enter commands and see the results — perfect for testing out simple code. You can also create separate files in which to store real Python programs by choosing File > New File in the REPL.

We'll use Python 3 rather than Python 2, as it is more up-to-date.

### Some teacher's notes

* When the tutorial starts to use indentation, the REPL starts to become annoying. At this point, use a dedicated Python file instead.
* To save a file, do File > Save As... and then choose somewhere memorable to save your file, like the desktop.
* To run your file, in the file window do Run > Run Module.
* To exit out of a running program, press Ctrl + C.

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

### Recursive function example

```
def greeting():
  name = input()
  print("Hello " + name + "! How are you?")
  greeting()

greeting()
```

### Simple random insult program

```
import random
insults = [
  "Your hair looks like a hedge",
  "Your feet smell of cheese",
  "Your nose could be used to vacuum the floor",
  "Your teeth look like tombstones",
]

def insult_me():
  rand = random.randint(0,len(insults)-1)
  print(insults[rand])

insult_me()

```

## See also

* [The Python tutorial](https://docs.python.org/3/tutorial/)
* [Learn Python](https://www.learnpython.org/)
* [Codecademy Learn Python](https://www.codecademy.com/learn/learn-python)
* [Raspberry Pi Foundation learning resources](https://www.raspberrypi.org/resources/learn/)
