# Python Turtle

Some of you have probably used [Turtle](https://en.wikipedia.org/wiki/Turtle_graphics) in your lessons — the drawing language that allows you to draw 2D patterns, spirals, shapes, etc.

Well, the good news is that Python on the Raspberry Pi features its own version of Turtle, which allows you to have fun drawing shapes and other things in the same way. In this lesson we will explore it.

## The basics of using Python Turtle

Let's start by creating a new Python file.

1. Open up Python 3 (IDLE), found in Programming > Python 3
2. Create a new file using File > New file
3. Use File > Save in the new window and save it as turtle-test.py in a sensible place, like Documents > python.

Important: Don't call your python files the same thing as modules you are using, such as turtle, random, time, etc. Modules are python files too, and so your file will conflict with the existing module name and cause an error.

Now let's write some code into our file.

First of all, enter the following line at the top of the file to import the turtle module:

```
import turtle
```

Next, we need to create an object representing a screen to draw onto, and an object representing the turtle itself, which will draw our shapes:

```
screen = turtle.Screen()
turtle = turtle.Turtle()
```

We can now start using methods of the ```turtle``` object to draw on the screen. Enter the following code loop to test whether our turtle is working ok:

```
for i in range(4):
  turtle.forward(100)
  turtle.right(90)
```

Try saving and running the script!

Once the drawing is done, you can close the window by pressing the x in the top right hand corner. Or you could add the following line to the bottom of the code, then save and run again:

```
screen.exitonclick()
```

Now you can close the drawing window by just clicking anywhere on the screen.

You have seen how to move forward 100 pixels and rotate the turtle to the right by 90 degrees. What commands do you think can be used to move the turtle backwards, and rotate to the left?

Try playing around for a bit, and drawing something different.

## Drawing different shapes

So far we've just drawn a square, but you can obviously draw other shapes too.

### Equilateral polygons

To draw another polygon with multiple sides the same length, you need to change the number of times it draws a side, and vary the angle it turns by after each iteration.

So for example to draw a hexagon, you need 6 sides, and a turn of 60 degrees each time. Some questions:

1. How did we work out the value of 60 degrees?
2. How do we change our loop to make it draw the hexagon

With those questions answered, try creating your hexagon.

Then try creating an octagon, a triangle, and a pentagon. Try something else if you like.

### Non-equilateral shapes

To create a non-equilateral shape, you'll obviously have to think a bit more carefully. The loop will no longer work, as you'll have to do different instructions for each side of the shape.

For example, to draw a trapezium, replace your loop with this:

```
turtle.forward(100)
turtle.right(60)
turtle.forward(100)
turtle.right(120)
turtle.forward(200)
turtle.right(120)
turtle.forward(100)
turtle.right(60)
```

Try drawing a different shape!

### Circles

Circles are easy in turtle. You have a defined ```circle()``` method that simply draws a circle. You just give it the radius of the circle to draw. Try replacing your shape with the following:

```
turtle.circle(100)
```

## Different colours

In Python, colours are represented by RGB (red, green, blue) values. By default the values accepted are between 0 and 1 (floating point numbers), but we want to use RGB values between 0 and 255, which is the standard accepted model used by web developers. To enable this, we need to first add the following line into our code:

```
screen.colormode(255)
```

Add this below the first three lines.

To change the colour of the turtle pen, you use the ```color()``` method. Try adding this into your code below the previous line you added:

```
turtle.color(255,0,0)
```

Note the American spelling. This is needed, otherwise it won't work.

To change the colour of your background, you use the ```bgcolor()``` method, which goes on the ```screen``` object, not the ```turtle``` object. For example, to change the colour to a nice light green:

```
screen.bgcolor(57,228,5)
```

Try adding this just after the previous line you added.

Have a play and see what colors you can come up with. There are many helpful tools online to help you choose colors, for example the [MDN color picker tool](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Colors/Color_picker_tool).

## Using a loop to make a cool pattern

Now we'll step things up a bit and use a loop to draw lots of shapes, making a cool pattern.

First, we'll turn our regular shape drawing into a function. You need to put all of your drawing lines inside a ```def``` block, like this:

```
def shape():
  lines
  are
  indented
  here
```

Once you've done that, create a loop like this:

```
for i in range(20)
  shape()
  turtle.right(5)
```

## Making your turtle go faster

So far I've only drawn 20 shapes, because it takes a long time for the turtle to draw them all. Imagine having 2000 shapes to draw?

Fortunately you can give your turtle a turbo boost. Try adding this line before any of your drawing code:

```
turtle.speed(0)
```

Now try running it again!

## Doing other things inside your loop

Now it's time to start having a play. You could try adding more iterations to your loop, e.g.

```
for i in range(100)
```

Don't go too crazy with the number!

You could try just drawing a single line then rotating, inside the loop:

```
for i in range(100)
  turtle.forward(100)
  turtle.right(67)
```

You can try increasing the length of the line and the color of the turtle by the value of i on each iteration:

```
for i in range(100)
  turtle.color(100 + i)
  turtle.forward(50 + i)
  turtle.right(67)
```

You can try setting a random color for each iteration:

```
from random import randint

...

for i in range(100)
  turtle.color(randint(0,255), randint(0,255), randint(0,255))
  turtle.forward(50 + i)
  turtle.right(67)
```

You can also try filling each shape you draw:

```
for i in range(100)
  turtle.begin_fill()
  turtle.color(100 + i)
  shape()
  turtle.end_fill()
  turtle.right(67)
```

Now try putting this all together to make something interesting. For example:

```
import turtle

screen = turtle.Screen()
turtle = turtle.Turtle()

screen.colormode(255)
screen.bgcolor(0,0,0)

turtle.speed(0)

def shape():
    turtle.forward(100)
    turtle.right(60)
    turtle.forward(100)
    turtle.right(120)
    turtle.forward(200)
    turtle.right(120)
    turtle.forward(100)
    turtle.right(60)

for i in range(36):
    turtle.begin_fill()
    turtle.color(30 + i*5, 0, i*4)
    shape()
    turtle.end_fill()
    turtle.right(10)

screen.exitonclick()
```

Try exploring the links below to see if you can find some other ideas, if there is time at the end of the lesson.

See also

* [The turtle API reference](https://docs.python.org/3/library/turtle.html)
* [Turtley amazing](https://projects.raspberrypi.org/en/projects/turtley-amazing)
* [Turtle snowflakes](https://projects.raspberrypi.org/en/projects/turtle-snowflakes/)
