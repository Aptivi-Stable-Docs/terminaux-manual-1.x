---
description: How does the color wheel work?
---

# ⛏ Color Wheel Internals

When you invoke the `InputForColor()` function, the library initializes the color wheel display to the console using an internal function, `RenderWheel()`. The color wheel then renders the current color in all the four modes:

1. Normal
2. Protanopia
3. Deuteranopia
4. Tritanopia

...using their rendered colors as the box color in an attempt to visualize what color is being used in the above modes.

The color wheel writes down the following information for each color mode:

1. Color RGB sequence
   * The color RGB sequence in the `RRR;GGG;BBB` format for VT sequences
2. HTML code
   * The color sequence in the HTML format `#FFFFFF` to facilitate usage for web development (HTML, CSS, ...)
3. Color type
   * This specifies the color type as follows:
     * `TrueColor`
     * `_255Color`
     * `_16Color`
   * This is inferred according to the color type, but it's usually the current color type for the color wheel.
4. Bright?
   * Find out if your selected color is bright or not.

The controls are then rendered. The color wheel waits for a keypress to do appropriate action. The controls are:

* `<-` and `->`
  * Changes the RGB mode
* `ARROW UP` and `ARROW DOWN`
  * Changes the color
* `CTRL + <-` and `CTRL + ->`
  * Changes the color blindness severity
* `TAB`
  * Changes the color mode
* `ESC`
  * Exits the color wheel
* `H`
  * Displays the help page
