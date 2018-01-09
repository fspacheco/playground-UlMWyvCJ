# What is a string in C

A string in C (also known as C string) is an array of characters, followed by a NULL character. To represent a string, a set of characters are enclosed within double quotes ("). The C string "Look Here" would look like as follows in memory:

```
-----------------------------------------
| L | o | o | k |  | H | e | r | e | \0 |
-----------------------------------------
```

It's an array of 10 characters.

## How to initialize a variable with C string

There are different ways to initialize a variable with C string.

```
char *char_ptr = "Look Here";
```

This initializes `char_ptr` to point to the first character of the read-only string `"Look Here"`. Yes, when a C string is initialized this way, trying to modify any character pointed to by `char_ptr` is undefined behaviour.

```C runnable
#include <stdio.h>

int main()
{
	printf("Look Here");
}

```
