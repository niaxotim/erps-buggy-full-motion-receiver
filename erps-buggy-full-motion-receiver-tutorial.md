### @activities true
### @explicitHints true

# ERPS STEM WEEK :: Motorised Buggy - Full Receiver

## Introduction
### Introduction Step @unplugged
We need to make our buggy respond to the full set of remote control commands to move; we've added 'left' and 'right' commands now.  

This tutorial goes with the simple tutorial on sending a fuller set of commands from the game controller.  

If you haven't done so yet, complete this tutorial first: [Full motion controller](https://makecode.microbit.org/#tutorial:github:niaxotim/erps-buggy-full-motion-controller/erps-buggy-full-motion-controller-tutorial)

![Motorised Buggy](https://raw.githubusercontent.com/niaxotim/erps-buggy-full-motion-receiver/master/assets/buggy_controller.png)

## Putting our buggy together!
### Assembling the pieces @unplugged
Before we start, make sure your buggy has been assembled. There are lots of sensors we *can* connect, but for now, just make
sure that the tyres are on the wheels, and that the wheels are connected to the motors.  
    
Oh, and don't forget some AA batteries too!

![Buggy Key Features](https://raw.githubusercontent.com/niaxotim/erps-buggy-full-motion-receiver/master/assets/features.png)


## Receiving new commands
### Step 1
Let's take our existing code, and expand it to be able to cope with the two new 'left' and 'right' commands that we're going
to be sending from our controller.  

Click on the '+' in your if-statement to add 2 more 'else-if' parts, and check if the 'name' variable is "left" or "right" for each one.  

#### ~ tutorialhint
```blocks
radio.onReceivedValue(function (name, value) {
    if (name == "forwards") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, value)
    } else if (name == "back") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, value)
    } else if (name == "left") {
    } else if (name == "right") {
    } else {
        Kitronik_Move_Motor.stop()
    }
})
```

### Step 2
Now we want to move the buggy either left or right, which is achieved by slowing down one of the wheels,
whilst continuing to move forwards.  

If we want to turn left, we slow down the left motor slightly, and if we want to turn right, we slow down the right motor.  

We can use the ``||Kitronik_Move_Motor:turn Left motor on direction Forward speed 0||`` block to achieve this, replacing
both the direction and speed.  

Drag 2 of these blocks in to your statement for turning left, and set one for the left motor, one for the right.

#### ~ tutorialhint
```blocks
radio.onReceivedValue(function (name, value) {
    if (name == "forwards") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, value)
    } else if (name == "back") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, value)
    } else if (name == "left") {
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorLeft, Kitronik_Move_Motor.MotorDirection.Forward, 0)
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorRight, Kitronik_Move_Motor.MotorDirection.Forward, 0)
    } else if (name == "right") {
    } else {
        Kitronik_Move_Motor.stop()
    }
})
```

### Step 3
As we said before, to turn left, we want to slow down the left motor a bit. We are going to set the speed
to *half* of that of the right motor.  

Drag a ``||math: 0 ÷ 0||`` divison block in to where the speed is set to 0, and on the left hand side of the sum,
place the 'value' variable (which represents our speed), and on the right, place a "2".  

#### ~ tutorialhint
```blocks
radio.onReceivedValue(function (name, value) {
    if (name == "forwards") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, value)
    } else if (name == "back") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, value)
    } else if (name == "left") {
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorLeft, Kitronik_Move_Motor.MotorDirection.Forward, value / 2)
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorRight, Kitronik_Move_Motor.MotorDirection.Forward, 0)
    } else if (name == "right") {
    } else {
        Kitronik_Move_Motor.stop()
    }
})
```

### Step 4
Finally, replace the '0' in for the speed of the 'right' motor with 'value' to set it to the speed we receive from the controller.  

#### ~ tutorialhint
```blocks
radio.onReceivedValue(function (name, value) {
    if (name == "forwards") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, value)
    } else if (name == "back") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, value)
    } else if (name == "left") {
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorLeft, Kitronik_Move_Motor.MotorDirection.Forward, value / 2)
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorRight, Kitronik_Move_Motor.MotorDirection.Forward, value)
    } else if (name == "right") {
    } else {
        Kitronik_Move_Motor.stop()
    }
})
```

### Step 5
Now repeat these blocks for changing the motor speed for the "right" direction.  

Remember to swap around which motor speed you will halve!  

Checkout out the hint if you get stuck!  

#### ~ tutorialhint
```blocks
radio.onReceivedValue(function (name, value) {
    if (name == "forwards") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Forward, value)
    } else if (name == "back") {
        Kitronik_Move_Motor.move(Kitronik_Move_Motor.DriveDirections.Reverse, value)
    } else if (name == "left") {
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorLeft, Kitronik_Move_Motor.MotorDirection.Forward, value / 2)
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorRight, Kitronik_Move_Motor.MotorDirection.Forward, value)
    } else if (name == "right") {
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorRight, Kitronik_Move_Motor.MotorDirection.Forward, value / 2)
        Kitronik_Move_Motor.motorOn(Kitronik_Move_Motor.Motors.MotorLeft, Kitronik_Move_Motor.MotorDirection.Forward, value)
    } else {
        Kitronik_Move_Motor.stop()
    }
})
```
### Step 6
That's it! Your buggy is ready to receive the two new "left" and "right" commands from your game controller.  

If you've extended your controller code to add even more features, now's the time to add them in to your buggy receiver!  

Perhaps you made the horn work? Or tried the lights?


### Step 7
Connect your BBC micro:bit and click ``|Download|`` to transfer your code.  

Put your micro:bit in to your buggy, and make sure it's switched on!  

Make sure your controller code is flashed and running, then give your controller buttons a press, including the new ones!  

Does your buggy move backwards and forwards as expected, *and* turn left and right?

### Buggy Full Motion Receiver Tutorial Complete @unplugged
Great work! You should now have a fully remote-controlled buggy moving in all directions! Woohoo!

![Great job](https://raw.githubusercontent.com/niaxotim/erps-buggy-full-motion-receiver/master/assets/great_job.png)
