# ASCII Image Converter

A Python script that converts an image into ASCII art by mapping pixel
brightness to characters.

## How it works

1. Load the image and resize it to a target width (default 80), scaling
   height proportionally with an aspect-ratio correction factor.
2. Convert it to grayscale so each pixel has a single brightness value (0-255).
3. Map each pixel's brightness to a character using a lookup table — darker
   pixels map to "denser" characters (`@`, `#`), lighter pixels map to
   sparser ones (`.`, ` `).
4. Print the result row by row to the terminal.

## Usage

```bash
uv add pillow
uv run python3 main.py
```

By default it reads `han.jpeg` from the same folder and prints ASCII art
to the terminal. Redirect to a file if you want to save it:

```bash
uv run python3 main.py > output.txt
```

## Example

```
----------------------------===+++====*&8###88&%+=----===-======================
--------------------------=+*%888#8888@@@@@@@@@@@8&*=---========================
-------------------------+&#@@@@@@@@@@@@@@@@@@@@@@@@#&+--=======================
-----------------------=%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@&+--=====================
----------------------=8@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#&=-====================
---------------------+#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#*---------===========
-------------------:+#@@@@@@@@@@@@@##@@@@@@@@@@@@@@##@@@@#@@&=---------=========
--------------:::::=#@@@@@@@@@@@@@@@#@@@@@@@@@@@@@@@@###@@##@8+-------==========
```
(Best viewed in a terminal — GitHub's proportional-width font may distort spacing.)

## Notes

- Brightness-to-character mapping uses a simple lookup table:
  `index = pixel * (len(ramp) - 1) // 255`, avoiding a long if/elif chain.
- Terminal characters are taller than they are wide, so image height is
  scaled by a 0.55 correction factor when resizing, to avoid a squashed
  output.

## Possible improvements

- Support arbitrary image filenames via command-line argument
- Add color support using ANSI escape codes
- Support video input (frame-by-frame conversion)