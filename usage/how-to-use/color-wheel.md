---
description: Here's how you can let the users choose their own colors
---

# 🎨 Color Wheel

## New Color Wheel

Starting from 1.9.0, the new color wheel, `ColorSelector`, is now available. You can use this brand new color selector to get information about your selected color visually. You can call the `OpenColorSelector()` function in your code to get the new color selector.

The color selector allows you to change the color in the following modes:

* In true color mode, you can change the hue, the lighting, and the saturation by pressing the appropriate key shortcuts to change the colors.
* In 256 and 16 colors mode, you can select a color using the right and the left arrow keys. It shows you color information, including the CMYK, HSL, and grayscale values.

The following controls are available:

| Key            | Action                                                                         |
| -------------- | ------------------------------------------------------------------------------ |
| `ENTER`        | Accept color selection                                                         |
| `ESC`          | DIscard changes                                                                |
| `H`            | Help page                                                                      |
| `LEFT`         | Reduce hue (for true color)                                                    |
|                | Previous color (for 256 and 16 colors)                                         |
| `CTRL + LEFT`  | Reduce lightness (true color only)                                             |
| `RIGHT`        | Increase hue (for true color)                                                  |
|                | Next color (for 256 and 16 colors)                                             |
| `CTRL + RIGHT` | Increase lightness (true color only)                                           |
| `DOWN`         | Reduce saturation (true color only)                                            |
| `UP`           | Increase saturation (true color only)                                          |
| `TAB`          | Change color mode (true color, 256 colors, and 16 colors)                      |
| `I`            | Shows the extended color information, including info about color deficiencies. |

## Old Color Wheel

{% hint style="warning" %}
This feature is available on 1.0.0 or higher. However, we discourage using it because it's obsolete and will be **removed** in the next Terminaux release. Obsoletion warnings were added in the last 1.x version series to guide developers to use the new color wheel.
{% endhint %}

This feature of Terminaux allows you to select a color from the color code (16 and 255 colors) or from the RGB levels (true color). It also allows you to get information about any color, similar to the color wheel function found in various web applications, including the built-in color blindness simulator located right in front of you.

For controls, the following keys do:

| Key                  | Action                                           |
| -------------------- | ------------------------------------------------ |
| `ESC`                | Exits the color selection                        |
| `ENTER`              | Accepts the color selection                      |
| `LEFT ARROW`         | Goes to the previous RGB level                   |
| `RIGHT ARROW`        | Goes to the next RGB level                       |
| `CTRL + LEFT ARROW`  | Decreases the color-blind severity               |
| `CTRL + RIGHT ARROW` | Increases the color-blind severity               |
| `TAB`                | Changes the color mode (16, 255, true)           |
| `UP ARROW`           | Increases the current RGB value of color         |
| `DOWN ARROW`         | Decreases the current RGB value of color         |
| `I`                  | Gives you more information about the colors used |

{% hint style="info" %}
By default, it starts in 16-color mode. If you want to use more than 16 colors, be sure to have a compatible console before trying to use the higher color spectrum.
{% endhint %}

When you invoke the color wheel from your application using one of the two overloads for the `InputForColor()` function, you'll most likely need to get its value, so you need to assign a color variable to the value of this function like so:

```csharp
var myColor = ColorWheel.InputForColor();
```

This is assuming that you've already imported the necessary namespace at the beginning of the C# code:

```csharp
using Terminaux.Colors.Wheel;
```

This function returns a `Color` instance containing necessary information. To know more about the structure of the `Color` class, visit the page below to learn more.

{% content-ref url="color-sequences.md" %}
[color-sequences.md](color-sequences.md)
{% endcontent-ref %}
