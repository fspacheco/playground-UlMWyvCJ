Examples in this lesson modifies existing string.

## String concatenation - `strcat`

The `strcat` function is used to append one string (source) at the end of another string (destination). It does the following:

1. Takes the destination string.
2. Finds the NULL character.
3. Copies the source string starting at the location of the NULL character of destination string.
4. Appends a NULL character to the destination string when all characters of the source string are copied to the destination string.

Here is an example:

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char src[] = "Look Here";
	char dest[40] = "Unimaginable";

	strcat(dest, src);
	printf("%s", dest);

	return 0;
}
```

Notice how it works. When `dest` is initialized with `char dest[40] = "Unimaginable";` there is a NULL character at the end. That's the starting point for the source string to be copied. When all characters of source string are copied to `dest`, a NULL character is appended.

**Warning:** The destination character array must be large enough to hold all characters of source, all characters of destination and a NULL character. Following ill-formed code triggers undefined behaviour:

```C
char src[] = "Look Here";
char dest[] = "Unimaginable";

/* strcat(dest, src); */ /* Fatal: dest doesn't have enough spaces to hold
                         all characters of dest
                         all chracters of src
                         a NULL character */
printf("%s", dest);
```

**Warning:** The destination character array must be initialized with C string before passing it to `strcat`. Following is an ill-formed code and shouldn't be practiced:

```C
char dest[40];

/* strcat(dest, "Look Here"); */ /* Fatal: dest is not initialized
                                 - no guarantee about a NULL character 
                                 - undefined behaviour */
/* printf("%s", dest); */ /* Fatal: dest isn't initialized - results in undefined behaviour */
```

At minimum the destination array could be initialized as empty string (only the NULL character) and after that `strcat` can be used:

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char dest[40] = "";

	strcat(dest, "Look Here");
	printf("%s", dest);

	return 0;
}

```

