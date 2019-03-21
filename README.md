# Macro Keyboard

some extra info on the Macro Keyboard

## Materials

### Keyboard PCB

The keyboard used is from Sergey Kiselev's Omega, which you can find [here](https://github.com/skiselev/omega).

## Building Procedure

### Keycap Layout

![](https://raw.githubusercontent.com/RedMikePumpkin/macro-keyboard/master/IMG_20190320_204334015.jpg)

```
Esc F1 F2 F3 F4 F5
~  1 2 3 4 5 6 7 8 9 0 - =  <-   Ins Home
Tab q w e r t y u i o p [ ]  \   Del End
Caps a s d f g h j k l ; ' Enter
Shift z x c v b n m , . / Shift     ^
Ctrl  Alt  Space   Fn Paste Win  <  v  >
```

### Arduino Wirings

if the keyboard header looks like
```
          .------- -------.
pin 15 -> |o o o o o o o o| <- pin 1
pin 16 -> |o o o o o o o o| <- pin 2
          '"""""""""""""""'
```
then the pinout is
```
Keyboard pin 1  -> Arduino pin 8
Keyboard pin 2  -> Arduino VCC
Keyboard pin 3  -> Arduino pin 9
Keyboard pin 4  -> Arduino pin 4
Keyboard pin 5  -> Arduino pin 10
Keyboard pin 6  -> Arduino pin 5
Keyboard pin 7  -> Arduino pin 11
Keyboard pin 8  -> Arduino pin 6
Keyboard pin 9  -> Arduino pin 12
Keyboard pin 10 -> Arduino pin 7
Keyboard pin 11 -> Arduino pin A0
Keyboard pin 12 -> Arduino pin A3
Keyboard pin 13 -> Arduino pin A1
Keyboard pin 14 -> Arduino pin A4
Keyboard pin 15 -> Arduino pin A2
Keyboard pin 16 -> Arduino GND
```

### Project Source

you can download the source by clicking "Clone or Download" -> "Download Zip" and extracting the zip into your downloads folder. The source is in a folder called "src"

### Replacing Macro Data

the `keyboards.json` file should look like this after getting to part 5f:

```
{"NAME":{"press":["TEXT"],"release":["TEXT"]}}
```

replace what is in the `{}` after the keyboard name, so

```
{"NAME":NEW DATA HERE}
```

is what it should look like. The new data can be found in `src/msx.txt`

## Software

there are 2 peices of software that I made for this project, the AVR code, and the Macro Processing code

### AVR code

the AVR code is what runs on the arduino, it:

1. Scans through every key on the keyboard, and reports any changes over Serial

2. Reads for macros from Serial, and executes them

it also does other data processing and I/O

#### Instructions and Formats

Keyboard I/O:

there are 4 Outputs, and 8 Inputs.
The outputs say a row ID (0 - 8) for the button matrix processor to look at.
The inputs are what keys are pressed on the row.

Scematic for keys and ID's can be found on the Omega page, linked earlier

Serial data sent out of the Arduino consists of a `p` or `r` (press or release) followed by 2 hexadecimal characters for the key ID. It ends with a newline character

Serial Input:

`m...\n`: the rest of the instruction until the newline is treated as a macro to execute

`nr\n`: returns the name of the keyboard over serial, prepended with `n` to say it's a name

`nw...\n`: the rest of the instruction until the newline is treated as the new name for the keyboard

Macro format:

`pXX`: press usb key with code XX (XX is in hexadecimal)

`rXX`: release usb key with code XX

`tXX`: press and release usb key with code XX
, 
`d####`: delay for #### ms (#### is in decimal)

### PC Software

It starts by scanning all of the open ports for anything starting with `/dev/ttyUSB`, `/dev/ttyACM`, or `COM`.

Then it polls every one with `nr\n` ("nr" followed by a newline) and looks for any responce for the next 50ms.

if it responds with something starting with an `n`, it displays the port.

When the user clicks on one of the ports, it starts reading the macros from the `keyboards.json` file, creating an empty entry if one doesn't exist.

There are some other buttons you can click in the keyboard menu, mainly changing some values.

When the program recieves Serial data while in the keyboard menu, it responds with the appropriate macro.
