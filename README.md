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
