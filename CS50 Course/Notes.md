# Big O Notation

Searching algorithm by dividing the amount of values in half each step has log2(n) complexity.

# Abstraction

It doesn't matter how a function is implemented, we can just use it as is. Applies to all type of operations, functions `print()` or `+`

`\` - escape sequence

# c
#c

Simple program in c language, called `hello_world.c`:
```c
#include <stdio.h>

int main(void)
{
	printf("hello, world\n");
}
```

`int main(void)`:
- `int` is the return type of the `main` function. It means that the function returns *integer* value
- `main` is the name of the function
- `(void)` is a list of parameters of the function. The `void` keyword means that the `main` function takes no arguments

In *c language* strings are marked with only double quotes `"some string"`.

To be able to run the program, it must be compiled first:
```bash
make hello_world
```

`make` is a simple program that runs `cc` compiler with required arguments. In other words, it runs the following code:
```bash
cc hello_world.c -o hello_world
```

As a result, an executable file `hello_world` is created.

Simple program with an input from a user:
```c
#include <stdio.h>

char str[100];

int main(void)
{
    printf("What's your name? ");
    scanf("%s", str);
    printf("hello, %s\n", str);
}
```

Another placeholders for `printf` are:
- `%i` for *integer*
- 