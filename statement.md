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

This initializes `char_ptr` to point to the first character of the **read-only** string `"Look Here"`. Yes, a C string initialized through a character pointer cannot be modified. When a C string is initialized this way, trying to modify any character pointed to by `char_ptr` is **undefined behaviour**. An undefined behaviour means that when a compiler encounters anything that triggers undefined behaviour, it is allowed to do anything it seems appropriate.

For example, the following C code crashes when compiled in Visual C++ 2017 when the commented out line is un-commented and the code is executed:

```C runnable
#include <stdio.h>

int main()
{
	char *char_ptr = "Look Here";

    /* Warning: uncommenting the following line will trigger undefined behaviour */
	/* char_ptr[5] = '_'; */
	printf("%s\n", char_ptr);

	return 0;
}

```

A more convenient way to initialize a C string is to initialize it through character array:

```
char char_array[] = "Look Here";
```

This is same as initializing it as follows:

```
char char_array[] = { 'L', 'o', 'o', 'k', ' ', 'H', 'e', 'r', 'e', '\0' };
```

But the former one is more intuitive. Note that when a character array is initialized by `char char_array[] = "Look Here";`, the terminating NULL character is appended automatically.

