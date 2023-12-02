---
description: May I read what you've written, please?
---

# 🖱 Input Reader

{% hint style="info" %}
This feature is available on 1.0.0 or higher.
{% endhint %}

This functionality is an important part of any interactive console application, because it gives users a chance to input what they want to write to the console.

You can easily use this feature in any interactive console application that uses Terminaux. Just use the `Terminaux.Reader` class that contains:

```csharp
public static string Read()
public static string Read(TermReaderSettings settings)
public static string Read(string inputPrompt)
public static string Read(string inputPrompt, TermReaderSettings settings)
public static string ReadPassword()
public static string ReadPassword(TermReaderSettings settings)
public static string ReadPassword(string inputPrompt)
public static string ReadPassword(string inputPrompt, TermReaderSettings settings)
public static string Read(string inputPrompt, string defaultValue, bool password = false, bool oneLineWrap = false, bool interruptible = false)
public static string Read(string inputPrompt, string defaultValue, TermReaderSettings settings, bool password = false, bool oneLineWrap = false, bool interruptible = false)
```

Each one of these functions creates a reader state, `TermReaderState`, that contains essential information about the current reader state, including, but not limited to:

* Current text
* Input prompt text
* Current text position
* Kill buffer
* Reader settings

Any key will append the selected characters to the current text input, and `RETURN` will accept the input. For more information about key bindings, go to the below page.

{% content-ref url="keybindings.md" %}
[keybindings.md](keybindings.md)
{% endcontent-ref %}

### History tools

{% hint style="info" %}
This feature is available on 1.6.0 or higher.
{% endhint %}

You can now set the history entry list with your array of history entries or clear the history list using the following functions:

* `SetHistory(List<string> History)`
  * Sets the history to the chosen history list
* `ClearHistory()`
  * Clears all history entries
