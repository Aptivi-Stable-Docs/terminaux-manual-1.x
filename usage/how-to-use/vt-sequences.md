---
description: We need to filter and build the VT sequences.
---

# 🗑 VT Sequences

{% hint style="info" %}
This feature is available on 1.0.0 or higher.
{% endhint %}

Alongside all the Terminaux features, VT sequences are the power of any terminal emulator found in literally every PC.

This feature provides several filtering and manipulation tools which allow you to perform these operations on strings that contain escape sequences under the `Terminaux.Sequences.Tools` namespace. Currently, these tools are provided:

| Function                           | Description                                                                            |
| ---------------------------------- | -------------------------------------------------------------------------------------- |
| `FilterVTSequences()`              | Filters all of the VT sequences                                                        |
| `MatchVTSequences()`               | Matches all of the VT sequences                                                        |
| `IsMatchVTSequences()`             | Does the string contain all of the VT sequences or a VT sequence of any type?          |
| `IsMatchVTSequencesSpecific()`     | Does the string contain all of the VT sequences or a VT sequence of any specific type? |
| `SplitVTSequences()`               | Splits all of the VT sequences                                                         |
| `DetermineTypeFromText()`          | Determines the VT sequence type from the given text                                    |
| `GetSequenceFilterRegexFromType()` | Gets the sequence filter regular expression from the provided VT sequence type         |

Place the `using Terminaux.Sequences.Tools;` directive at the top of the file that you want to call these functions in. You need to put the class name `VtSequenceTools` before the function name mentioned above so that it looks like this:

<pre class="language-csharp"><code class="lang-csharp">char BellChar = Convert.ToChar(0x7);
char EscapeChar = Convert.ToChar(0x1b);
char StringTerminator = Convert.ToChar(0x9c);
string vtSequence1 = $"{EscapeChar}[38;5;43m";
<strong>string filtered = VtSequenceTools.FilterVTSequences($"Hello!{vtSequence1}");
</strong><strong>Console.WriteLine(filtered);
</strong></code></pre>

### Sequence builder

offers a Builder namespace that contains building blocks for building a VT sequence for your console applications.

It starts with `VtSequenceBasicChars` which allows you to get a variety of starting-point characters for your VT sequence in case you want to manually build the sequence yourself. Here are the available characters:

* `BEL (\x07 - CTRL+G - BellChar)`
* `BS (\x08 - CTRL+H - BackspaceChar)`
* `CR (\x0D - CTRL+M - CarriageReturnChar)`
* `ENQ (\x05 - CTRL+E - ReturnTerminalStatusChar)`
* `FF (\x0C - CTRL+L - FormFeedChar)`
* `LF (\x0A - CTRL+J - LineFeedChar)`
* `SI (\x0F - CTRL+O - StandardCharacterSetChar)`
* `SO (\x0E - CTRL+N - AlternateCharacterSetChar)`
* `SP (" " - SPACE - SpaceChar)`
* `TAB (\x09 - CTRL+I - HorizontalTabChar)`
* `VT (\x0B - CTRL+K - VerticalTabChar)`
* `ESC (\x1B - VerticalTabChar)`
* `ST (\x9C - VerticalTabChar)`

Each type of VT sequence contain their own class files that stores both the regex match information about specific actions and sequence generation functions based on the given action and argument. Here are a list of supported sequence types:

* APC sequences
  * Application program command
* C1 sequences
  * 8-bit control characters
* CSI sequences
  * Controls beginning with control sequence introducer
* DCS sequences
  * Device control
* ESC sequences
  * Controls beginning with ESC
* OSC sequences
  * Operating system command sequences
* PM sequences
  * Privacy message

To learn more about these sequences, visit the below page:

{% embed url="https://invisible-island.net/xterm/ctlseqs/ctlseqs.html" %}

The builder also provides a powerful tool which allows you to build almost any VT sequence using only the arguments and the specific type of VT sequence (Character attributes for example). This tool is found inside the `VtSequenceBuilderTools` class under the `Terminaux.Sequences.Builder` namespace.

Currently, it provides these tools:

* `BuildVtSequence(VtSequenceSpecificTypes specificType, params object[] arguments)`
  * Allows you to build your VT sequence
  * Returns a string consisting of a VT sequence of the requested type with the requested arguments
* `DetermineTypeFromSequence(string sequence)`
  * Allows you to determine the type from a specific VT sequence
  * Returns a tuple of `(VtSequenceType, VtSequenceSpecificTypes)` which holds both the broad VT sequence type (CSI for example) and the specific type (Character attribute for example).
