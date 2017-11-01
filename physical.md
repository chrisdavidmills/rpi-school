# Physical computing with Python

Now we've had fun programming Minecraft with Python, let's now look at using this very versatile language to do something else. In this lesson we'll look at Physical computing, i.e. the process of controlling hardware with code.

## Another look at the connector pins

At the start of the course we looked at the connector pins. These allow you to connect hardware devices directly to the Pi's motherboard. This is really cool, as it allows you to do your own electronics experiments. It has power pins (to provide power), ground pins (to complete a circuit), and GPIO pins (that allow hardware to be controlled with code).

Take the top off your Pi and you will see them, in two rows of 20, on one edge of the Pi's motherboard.

It looks like this (image borrowed from the Raspberry Pi Foundation):

![](pinout.png)

We will be plugging some wires and components into these pins to have some fun with electronics.

<strong>A very important note — follow the instructions carefully in this section of the course. If you get code wrong, you will probably just get an unexpected result. If you plug electronic components into the wrong place, you can can actually damage them, or the Pi itself.</strong>

<strong>DO NOT PLUG THINGS IN RANDOMLY — FOLLOW THE INSTRUCTIONS!</strong>

## Basic work with an LED

In this section, we'll follow the [Physical Computing with Python](https://projects.raspberrypi.org/en/projects/physical-computing) course from the Raspberry Pi Foundation — these sections:

* Light an LED
* Switching an LED on and off
* Flashing an LED sections.

Watch me do each step first, then you have a go.

### Basic notes about electronics

1. LEDs have to be connected to a circuit in one direction — the power has to be connected to the longer leg, and the earth to the shorter leg.
2. You also need to use a resistor, to limit the amount of current going into the LED, otherwise it will pop! Anything over about 50 ohms will do. You need to put the resistor before the LED in the circuit.
3. The current flows from the power supply (orange, red, or yellow pin) to the ground (black pin).
4. Always use the same colour to go from your power supply pin, and the same colour to go to your ground, e.g. blue from power, and black to ground.
5. To work out the strength of a resistor, you need to read the coloured bands — [How to Read Axial Lead Resistors](https://www.wikihow.com/Read-Axial-Lead-Resistors) will help you out. For these simple LED examples, about 330 ohms is good.
6. Using a breadboard is the easiest way to create a circuit. The metal strips run horizontally across the board; you can use each set of 5 holes as a connector for one part of the circuit.

### A slightly more complex LED sequence

```
from gpiozero import LED
from time import sleep

led = LED(17)

while True:
    led.on()
    sleep(0.5)
    led.off()
    sleep(0.2)
    led.on()
    sleep(0.2)
    led.off()
    sleep(0.2)
    led.on()
    sleep(0.5)
    led.off()
    sleep(0.2)
```

### Multiple LEDS - traffic lights

Now let's try something a bit more real — a traffic light sequence.

First, the hardware:

1. Stop your previous program running by going to the Python shell and pressing Ctrl + C.
2. Find out a red, yellow, and green LED, two more 330 ohm resistors, and four more jump leads.
3. Replace your current LED with a red one, remembering to put it in the right way. To recap, this one is plugged in at GP17 (left, 6th pin) and GND (right, 3rd pin)
4. Make a copy of the existing circuit, using GP18 (right, 6th pin) and GND (right, 7th pin). Test it by running the existing example on it, substituting LED(17) for LED(18)
5. Make another copy of the existing circuit, using GP11 (left, 12th pin) and GND (left, 13th pin). Test it by running the existing example on it, substituting LED(17) for LED(11)

Now, the code:

Create a new file called traffic_lights.py, then enter the following code to start:

```
from gpiozero import LED
from time import sleep

red = LED(17)
amber = LED(18)
green = LED(11)
```

below the previous code, enter the following:

```
while True:
  redToGreen()
  greenToRed()
```

Now we'll define each of the two functions invoked in the above loop.

First, ```redToGreen()```:

```
def redToGreen():
  red.off()
  sleep(5)
  amber.on()
  sleep(5)
  red.off()
  amber.off()
  green.on()
  sleep(15)
```

Now, ```greenToRed()```:

```
def greenToRed():
  green.off()
  sleep(5)
  amber.on()
  sleep(5)
  amber.off
  sleep(5)
  red.on()
  sleep(15)
```


# See also

[Physical Computing with Python](https://projects.raspberrypi.org/en/projects/physical-computing)
