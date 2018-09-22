# Language Flags

One place where Koi shines, is in its' ability to customise how the compiler or interpreter work, through language flags. These will either come with the standard library, or can be included in libraries.

Core features such as the garbage collector and pre-processor are registered simply as a togglable flag, but packages can be built for flags, allowing for entries with-in a "flag class" to be changed.

An example of a language flag, could be like this:

```text
package test::flags

import console::println

flag PrintHello() {
    call println("Hello, World!")
}
```

Then, when the flag was toggled, like so:

```text
import test::flags::PrintHello

@PrintHello
```

Now, when the program that contains this is run, "Hello, World!" will be printed to the terminal.

But you can also create flags that can be toggled on or off, like so:

```text
package test::flags

toggle flag MyToggle(value: bool) {
    if (value) {
        print("MyToggle on!")
    }
    else {
        print("MyToggle off!")
    }
}
```

Which can then be toggled and untoggled like so:

```text
import test::flags::MyToggle

@MyToggle
# Prints "MyToggle on!"
@!MyToggle
# Prints "MyToggle off!"
```

