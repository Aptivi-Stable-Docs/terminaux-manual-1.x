---
description: How does this feature work?
---

# 🔧 Color Sequences Internals

There are three stages in which ColorSeq does to generate a new instance of the `Color` class.

## Stage 1: Parsing

When making a new instance of the `Color` class, it converts the input to the equivalent color specifier string, which then gets parsed.

### `RRR;GGG;BBB`

If the color specifier contains the semicolon `;` delimiter, the constructor attempts to validate the specifier to check to see if there are exactly three values (RGB)

If valid, it checks the three numbers to check to see if they are within the range of 0 to 255. If all these numbers are valid, the builder then goes on to perform Stage 2.

### `<num>` or `<ColorName>`

If the color specifier is of the type `<num>` or `<ColorName>`, it makes a new instance of the `ConsoleColorsInfo` class that contains necessary data to build the `Color` instance.

It checks the three numbers to check to see if they are within the range of 0 to 255. If all these numbers are valid, the builder then goes on to perform Stage 2.

### `#000000`

If the color specifier is of this type, the library gets the RGB values by attempting to shift the bytes like this:

```csharp
int ColorDecimal = Convert.ToInt32(ColorSpecifier.RemoveLetter(0), 16);
R = (byte)((ColorDecimal & 0xFF0000) >> 0x10);
G = (byte)((ColorDecimal & 0xFF00) >> 8);
B = (byte)(ColorDecimal & 0xFF);
```

This assumes that the colors are valid. The builder goes on to perform Stage 2.

## Stage 2: Transforming

If color transformation is enabled, the library selects the formula used to make transformations, depending on the value of `EnableSimpleColorTransformation`.

* If the simple color transformation is enabled, the color transformation is done according to the Vienot 1999 formula.
* If the simple color transformation is disabled, the color transformation is done according to the Brettel 1997 formula.

After transformation is done, the resulting values are installed to the main RGB values.

## Stage 3: Installation

The library attempts to install the necessary values for color information, the most important being:

* `PlainSequence`
* `PlainSequenceEnclosed`
* `VTSequenceForeground`
* `VTSequenceBackground`
* `Type`
  * `TrueColor`
  * `_255Color`
  * `_16Color`

You can also use the following values:

* `IsBright`
* `IsDark`
* `Hex`
