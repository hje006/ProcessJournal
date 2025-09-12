# Initial Concept
![Inital Concept Sketch](./Images/BreathReminderDrawing.png)

# Code Concept
pusedo code here
Diagram with microbit and values

# Code Progress
## Version 1
```
let speed = 0
let currentZ = 0
let lastZ = input.acceleration(Dimension.Z)
basic.forever(function () {
    currentZ = input.acceleration(Dimension.Z)
    speed = currentZ - lastZ
    lastZ = currentZ
    speed = speed / 1
    if (speed >= 1) {
        speed = speed - 1
    } else {
        if (speed < 0) {
            speed = speed + 1
        }
    }
    // Send to simulator/USB serial console
    serial.writeValue("speed", speed)
    basic.pause(1)
})
```
used to get variables of speed for breathing, used for inital speed calculations and filtering.

(image of speed waves from website here)

## Version 2
```
let lastZ = input.acceleration(Dimension.Z)
let speed = 0

// Standard breathing threshold
let THRESHOLD = 80      // central mg
let RANGE = 40          // +/- leeway

basic.forever(function () {
    let currentZ = input.acceleration(Dimension.Z)
    speed = currentZ - lastZ
    lastZ = currentZ

    let absSpeed = Math.abs(speed)

    if (absSpeed >= (THRESHOLD - RANGE) && absSpeed <= (THRESHOLD + RANGE)) {
        // breathing detected
        basic.showIcon(IconNames.Heart)   // show breathing
        serial.writeValue("breath", speed)
    } else {
        basic.showIcon(IconNames.SmallDiamond) // idle / no breathing
        serial.writeValue("breath", 0)
    }

    basic.pause(200)
})
```
used to introduce a cleaner more effective speed filter with acceptable leeway, less messy and uses larger numbers to calculate breathing meaning faster and slower movements are less likley to be picked up by the microbit.

## Version 3
code and comments
Time Filter (WIP)

# Prototype
image here
whats new