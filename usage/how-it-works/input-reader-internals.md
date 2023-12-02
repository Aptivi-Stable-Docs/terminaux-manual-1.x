---
description: What's exactly going on?
---

# 🪛 Input Reader Internals

When the `Read()` function gets called, it first creates a new instance of `TermReaderState` to store the state of the current terminal input session. Then, it writes the input prompt to the console.

Before prompting for input, it initializes the current terminal reader state. TermRead then waits for a struck key before processing it by the keybinding reader, `BindingsReader`, which calls `Execute()`.

To execute, `BindingsReader` has to look for any matching keybindings in two places:

* Base bindings
* Custom bindings

...by checking the `BindMatched()` value. In case none of the bindings match the key pressed, it falls back to the `InsertSelf()` binding.

After the matching keybinding is found, it goes on to perform the action defined by the overridden `DoAction(TermReaderState)` function with the current `TermReaderState` instance.

It repeats the above steps for any key pressed until one of the keys is a terminating keybinding, which usually sets the `IsExit` value to `true`. In this case, when `IsTerminate(ConsoleKeyInfo)` returns true, TermReader stops processing any further keys.

It then seeks the console cursor to the end of the text and writes a new line to the console, signifying that the input is aborted.

Depending on the `defaultValue` argument, if there is no current text, it goes on to replace the input with the `defaultValue`.

Then, it checks to see if the terminal reading mode isn't a password mode and if the history is enabled. If it's satisfied, it adds the input to the history.

Finally, it resets the terminal state and returns the written input.
