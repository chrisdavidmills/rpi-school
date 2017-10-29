# Programming Minecraft

The last lesson was a bit boring, wasn't it? Well, you need to learn to walk before you can fly.

Now you've got used to what Python looks like, you'll have a look at the special version of Minecraft available on the Pi, and look at how we can start to program it.

## Getting used to Minecraft Pi

1. From the main Pi menu, choose Games > Minecraft Pi.
2. From the Minecraft main screen, choose Start Game, then choose Create new from the Select world screen.
3. Let's have a quick play to familiarise ourselves with the controls.

* Look around with the mouse
* Left mouse button — smash blocks
* Right mouse button — place block/hit with sword/fire bow
* 1-8 — select items in inventory
* WASD — move forward/left/back/right
* E — inventory
* Double tap space — start/stop flying
* When on ground, Shift is crouch, and space is jump
* When flying, Shift is descend, and space is ascend
* Esc — menu
* Tab — go out of Minecraft, and control the rest of the Pi desktop

## Starting to program Minecraft Pi

To program Minecraft Pi, we need to use Python.

1. Press the Tab key to get out of the Minecraft program but still leave it running in the background.
2. Load up Python 3 again (Programming > Python 3 in the main Pi menu). Create a new file with File > New File.
3. Save it as mcpi-test.py, in Documents/minecraft.

Like we briefly looked at in the previous lesson, we need to import a module to allow us to access the Minecraft world from Python. Enter the following line in your new file:

```
from mcpi.minecraft import Minecraft
```

Next, enter the following line that creates an instance of the Minecraft world that we can start to do things to:

```
mc = Minecraft.create()
```

Now, to make the program do something and test it out, put the following line below the two others:

```
mc.postToChat("Hello , I'm in Minecraft!")
```

## Setting and getting player position

You can use ```player.getPos()``` and ```player.setPos()``` to get and set your character's position in the world. For example, replace the ```postToChat()``` line with the following two lines:

```
x, y, z = mc.player.getPos()
print("Player is at position " + str(x) + ", " + str(y) + ", " + str(z) + ".")
```

Now add the following below the previous two lines:

```
mc.player.setPos(x, y+100, z)
```

## Creating blocks

You can create a single block using the ```setBlock()``` function. Try deleting the ```setPos()``` line, and replacing it with this one:

```
mc.setBlock(x+1, y, z, 1)
```

You can create several blocks in a big solid cube using ```setBlocks()```, so for example:

```
mc.setBlocks(x+1, y+1, z+1, x+6, y+6, z+6, 1)
```

The first parameters set the position of the block (or blocks), while the last parameter sets the type of block to draw. Block ID 1 is stone. Try others, as specified in this [Raspberry Pi Minecraft Block ID Number Reference](https://www.raspberrypi-spy.co.uk/2014/09/raspberry-pi-minecraft-block-id-number-reference/). I'm sure you'll all be big fans of block 46!

You can also get blocks in a slightly more readable way — using block constants. Add the following line just below the first import line:

```
from mcpi import block
```

Now you can retrieve block IDs via more understandable keywords, for example:

```
mc.setBlock(x+1, y, z, block.GLOWSTONE_BLOCK.id)
```

You still need to put ```.id``` on the end of it to access the ID, which is what the ```setBlock()``` method expects.

## Putting this together

Let's look at a couple of fun examples. First of all, I got this from the [Getting Started with Minecraft Pi](https://projects.raspberrypi.org/en/projects/getting-started-with-minecraft-pi) tutorial from Raspberry Pi Foundation:

```
from mcpi.minecraft import Minecraft
from mcpi import block
from time import sleep

mc = Minecraft.create()

while True:
    x, y, z = mc.player.getPos()
    mc.setBlock(x, y, z, block.FLOWER_YELLOW.id)
    sleep(0.1)
```

This constantly grows flowers behind you as you walk around. ```while True``` always returns true, so the program runs forever (you can stop it by going to the REPL and pressing Ctrl + C).

Can you try to change it so that when you walk along, a red carpet is put down beneath you? remember that y is the coordinate that states how far up or down a position is.

### detecting the block beneath you

In this example we detect the block we are stood upon. If it is grass, we plant a carpet of flowers around us:

```
from mcpi.minecraft import Minecraft
mc = Minecraft.create()

grass = 2
flower = 38

while True:
    x, y, z = mc.player.getPos()  # player position (x, y, z)
    block_beneath = mc.getBlock(x, y-1, z)  # block ID
    print(block_beneath)

    if block_beneath == grass:
        mc.setBlocks(x-1, y, z-1, x+1, y, z+1, flower)
```

### Random lava!

Let's add a bit of excitement into the game, by spawning random lava above you every so often:

```
from mcpi.minecraft import Minecraft
import random
mc = Minecraft.create()

lava = 10

while True:
    x, y, z = mc.player.getPos()  # player position (x, y, z)
    block_beneath = mc.getBlock(x, y-1, z)  # block ID
    print(block_beneath)

    rand = random.randint(0,100)
    if rand == 50:
        mc.setBlock(x, y+10, z, lava)
```

### Building a house

The following script builds an entire house right next to you in the minecraft world!

```
import mcpi.minecraft as minecraft
import time
import mcpi.block as block
if __name__ == "__main__":
        time.sleep(2)
        mc = minecraft.Minecraft.create()
        mc.postToChat("Starting now!")
        time.sleep(1)
        playerPosition = mc.player.getPos()
        playerPosition = minecraft.Vec3(int(playerPosition.x), int(playerPosition.y), int(playerPosition.z))
        mc.setBlocks(playerPosition.x+1, playerPosition.y, playerPosition.z+1, playerPosition.x+9, playerPosition.y, playerPosition.z+9, block.COBBLESTONE)  
        mc.setBlocks(playerPosition.x+1, playerPosition.y+1, playerPosition.z+1, playerPosition.x+9, playerPosition.y+1, playerPosition.z+1, block.WOOD)
        mc.setBlocks(playerPosition.x+9, playerPosition.y+1, playerPosition.z+1, playerPosition.x+9, playerPosition.y+1, playerPosition.z+9, block.WOOD)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+1, playerPosition.z+9, playerPosition.x+1, playerPosition.y+1, playerPosition.z+1, block.WOOD)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+1, playerPosition.z+9, playerPosition.x+9, playerPosition.y+1, playerPosition.z+9, block.WOOD)
        time.sleep(3)
        mc.setBlock(playerPosition.x+1, playerPosition.y+1, playerPosition.z+5, block.AIR)
        mc.setBlock(playerPosition.x+0, playerPosition.y, playerPosition.z+5, block.STONE_SLAB)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+2, playerPosition.z+1, playerPosition.x+9, playerPosition.y+2, playerPosition.z+1, block.WOOD)
        mc.setBlocks(playerPosition.x+9, playerPosition.y+2, playerPosition.z+1, playerPosition.x+9, playerPosition.y+2, playerPosition.z+9, block.WOOD)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+2, playerPosition.z+9, playerPosition.x+1, playerPosition.y+2, playerPosition.z+1, block.WOOD)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+2, playerPosition.z+9, playerPosition.x+9, playerPosition.y+2, playerPosition.z+9, block.WOOD)
        time.sleep(3)
        mc.setBlock(playerPosition.x+1, playerPosition.y+2, playerPosition.z+5, block.AIR)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+4, playerPosition.z+1, playerPosition.x+9, playerPosition.y+4, playerPosition.z+9, block.GLOWSTONE_BLOCK)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+3, playerPosition.z+1, playerPosition.x+9, playerPosition.y+4, playerPosition.z+1, block.WOOD)
        mc.setBlocks(playerPosition.x+9, playerPosition.y+3, playerPosition.z+1, playerPosition.x+9, playerPosition.y+4, playerPosition.z+9, block.WOOD)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+3, playerPosition.z+9, playerPosition.x+1, playerPosition.y+4, playerPosition.z+1, block.WOOD)
        mc.setBlocks(playerPosition.x+1, playerPosition.y+3, playerPosition.z+9, playerPosition.x+9, playerPosition.y+4, playerPosition.z+9, block.WOOD)
        time.sleep(3)
        mc.setBlock(playerPosition.x+1, playerPosition.y+1, playerPosition.z+5, block.AIR)
        mc.setBlock(playerPosition.x+1, playerPosition.y+2, playerPosition.z+5, block.AIR)
        mc.setBlock(playerPosition.x+8, playerPosition.y+1, playerPosition.z+5, block.CRAFTING_TABLE)
        mc.setBlock(playerPosition.x+8, playerPosition.y+1, playerPosition.z+6, block.FURNACE_ACTIVE)
        mc.setBlock(playerPosition.x+8, playerPosition.y+1, playerPosition.z+4, block.FURNACE_ACTIVE)
        mc.setBlock(playerPosition.x+8, playerPosition.y+1, playerPosition.z+7, block.CHEST)
        mc.setBlock(playerPosition.x+8, playerPosition.y+1, playerPosition.z+3, block.CHEST)
        time.sleep(2)
        mc.player.setPos(playerPosition.x+3, playerPosition.y+4, playerPosition.z+3)
```

# See also

* [Getting Started with Minecraft Pi](https://projects.raspberrypi.org/en/projects/getting-started-with-minecraft-pi)
* [Minecraft Pi API reference](http://www.stuffaboutcode.com/p/minecraft-api-reference.html)
