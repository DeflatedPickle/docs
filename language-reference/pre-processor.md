# Pre-Processor

Like C++, Koi has a pre-processor, that is shared across any possible implementations.

The pre-processor is mostly used for macros, that will be transpiled when the code is run. The compiler or interpreter will run the code through the pre-processor then run the output to the compiler or interpreter, if the language flag is turned on.

An example of something implemented through the pre-processor could be the range syntax, which would be written as so:

```text
0 to 5
```

And could be implemented like so:

```text
macro range(first: int, type: str, second: int): int[] = [first={int}, type={"to"|"until"}, second={int}] {
    val list = []
    
    var num = first + 1 if type == "to" else first
    
    while num < second + 1 {
        call list.append(num)
        num += 1
    }
    
    return list
}
```

This would then, after being run through the pre-processor, would be transpiled to:

```text
[0, 1, 2, 3, 4, 5]
```

