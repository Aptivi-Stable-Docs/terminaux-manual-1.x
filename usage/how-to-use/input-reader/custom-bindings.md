---
description: How to assign your own binding?
---

# 🔌 Custom bindings

TermRead supports custom bindings, which you can assign your `BaseBinding` class containing the following functions you must override:

* `BoundKeys`
  * This holds all the keys to bind your custom action to.
* `DoAction(TermReaderState)`
  * This is the heart of your key binding. You can do anything with the text using the current terminal reader state.

You can also override these:

* `IsExit`
  * If `true`, causes TermRead to assume that the input is done after executing the action that this binding implements.
* `BindMatched(ConsoleKeyInfo)`
  * Specify your own method on how to check to see if the input key matched all the bound keys (`BoundKeys`) in your custom key binding.

## Principles

Your keybinding must follow the below principles:

* For text positioning, you must use any function in the `PositioningTools` class.
* For manual console manipulation, you must use any function in the `ConsoleWrapperTools` class.
* Your bound key must not be already bound to a key that was already bound by either a base or another custom binding, or two bindings execute at the same time, potentially causing conflict.
* To manipulate with text, you must use the `state.CurrentText` property.

At the end, your base class must look like this at minimum:

```csharp
using System;
using Terminaux.Reader;
using Terminaux.Reader.Tools;

namespace MyApp
{
    internal class MyBinding : BaseBinding, IBinding
    {
        public override ConsoleKeyInfo[] BoundKeys { get; } = 
        {
            // All keys listed below will lead to the below DoAction being executed.
            new ConsoleKeyInfo('\0', ConsoleKey.Key, false, false, false)
        };

        public override void DoAction(TermReaderState state)
        {
            // Your action.
        }
    }
}
```

where:

* `ConsoleKey.Key`
  * Any console key. Consult the [documentation](https://learn.microsoft.com/en-us/dotnet/api/system.consolekey) for more info.
* `\0`
  * A character that must match the corresponding `ConsoleKey.Key`.

{% hint style="info" %}
If you're assigning a key containing `CTRL`, you must assign a character number starting from `0x0`. For example, `CTRL+Y` is `\u0019`.
{% endhint %}

## How to bind

Once you created a base class as mentioned above, you can finally use the `CustomBindings` class to call the `Bind(BaseBinding)` function to add your own binding to the custom binding store, like this:

```csharp
CustomBindings.Bind(new MyBinding());
```

{% hint style="warning" %}
**Warning:** You must call this function once. It does nothing if your binding is already installed.
{% endhint %}

To remove binding, you must use the `Unbind(ConsoleKeyInfo)` command.
