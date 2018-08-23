# Getting Started

## Hello World

To get started using the Koi language, you should first take a look at the language and library references. After that, it's recommended to install a text editor or IDE that supports the Koi language \(plugins and this list will come later\). You'll also want to install the Koi language, which can be found on the website \(in the future\).

You'll most likely then want to write the most basic form of program, to get used to the language. This being a "Hello World" program \(a program that simply prints "Hello, World!" to the terminal.

To write such a program in Koi, you'll first want to create a file with the extension ".koi". In this file, you'll want to start by creating a main procedure. This will be the entry point of the program. To do this, you'll want to type:

```text
pro main() {
}
```

Since you want to print, you'll need to import the console library, a library for working with the terminal/console. To do this, at the top of your file \(before the main procedure\):

```text
import console
```

This will then import the console package. To access the print procedure from the console package, you'll want to, inside of the main procedure, type:

```text
console::println("Hello, World!")
```

Now you should have a file that looks like this:

```text
import console

pro main() {
    console::println("Hello, World!")
}
```

To run the file, you'll either want to use the run command from your IDE \(if supported\) or run the file from the terminal \(documentation for the CLI will come later\).

After running, you should see "Hello, World!" printed to the terminal. Great!

### Alternatives

Instead of using a procedure for `main`, you could instead use a subroutine or a function. Using a subroutine would work in the same way, however a function would require you to return a value, preferably an integer, which would be used to show the exit status of the program. When using a procedure, this value defaults to 0, which is considered a sucsessful exit.

And instead of having to preface `println` with `console` each time, you could instead use:

```text
import println from console
```

To import just the `println` function from package, meaning you would only have to do:

```text
println("Hello, World!")
```

## Arithmetic Machine

After learning how to print in Koi, and using the basics of the main entry point, next, we can look at entry arguments. These are arguments that are supplied when running the program through a terminal and accepted and used by the program.

To accept command-line arguments in our entry point, we will need to specify a variable of the type they should be. If you would like a single string, it should be a single string argument. If you would like a list of strings, it should be a list of the string type. Any type works, really. As long as the command-line argument can be cast to it or appended to it.

For the basic version, we will be accepting 2 integers and a string for the kind of arithmetic opperation to perform.

```text
pro main(first: int, second: int, type: str) {
}
```

Now that our program accepts the arguments, we can implement how it uses them. For this, I'm going to print out the formula and the result \(this solution is most likely not the best\).

```text
import console

pro main(first: int, second: int, type: str) {
    var result = 0
    switch type {
        case "+" { result = first + second }
        case "-" { result = first - second }
        case "*" { result = first * second }
        case "/" { result = first / second }
    }

    console::print("#{first} #{type} #{second} = #{first }")
}
```

We can then, from the command-line \(or a scripting language like Batch and Bash\), call the compiler to compile the program with the given arguments:

```text
koi main.koi 5 5 +
```

And it should print: `5 + 5 = 10`

### Extensions

* Accept a list of integers and add them all together

