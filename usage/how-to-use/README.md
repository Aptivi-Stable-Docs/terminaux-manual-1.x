---
description: How do you use it?
---

# 🖥 How to use

To use this library, you first need to know exactly why do you need to install Terminaux into your console application. If your application is intended to be an interactive one, or if your application shows graphics (text, info box, ...), then Terminaux is the right library for you.

Terminaux provides several terminal actions, like reading an input (was on TermRead), getting color information (was on ColorSeq), and using VT sequences and filtering them (was on VT.NET).

For complete overview of functionality, consult the below pages:

{% content-ref url="input-reader/" %}
[input-reader](input-reader/)
{% endcontent-ref %}

### Reading an input

Just use the `Terminaux.Reader` class that contains:

* `Read()`
* `Read(string)`
* `Read(string, string, bool, bool)`
* `ReadPassword()`
* `ReadPassword(string)`

Each one of these functions creates a reader state, `TermReaderState`, that contains essential information about the current reader state, including, but not limited to:

* Current text
* Input prompt text
* Current text position
* Kill buffer

Any key will append the selected characters to the current text input, and `RETURN` will accept the input. For more information about key bindings, go to the below page.

{% content-ref url="input-reader/keybindings.md" %}
[keybindings.md](input-reader/keybindings.md)
{% endcontent-ref %}

{% content-ref url="color-sequences.md" %}
[color-sequences.md](color-sequences.md)
{% endcontent-ref %}

{% content-ref url="vt-sequences.md" %}
[vt-sequences.md](vt-sequences.md)
{% endcontent-ref %}

{% content-ref url="color-wheel.md" %}
[color-wheel.md](color-wheel.md)
{% endcontent-ref %}

{% content-ref url="console-writers.md" %}
[console-writers.md](console-writers.md)
{% endcontent-ref %}

{% content-ref url="figlet-font-selector.md" %}
[figlet-font-selector.md](figlet-font-selector.md)
{% endcontent-ref %}

{% content-ref url="console-size-requirements.md" %}
[console-size-requirements.md](console-size-requirements.md)
{% endcontent-ref %}
