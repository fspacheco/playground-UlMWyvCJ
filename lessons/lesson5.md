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

**Warning:** The destination character array must be initialized with C string before passing it to `strcat`. In other words, the destination character array must have at least 1 location which has a NULL character. Following is an ill-formed code and shouldn't be practiced:

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

Character pointers can be used in `strcat`:

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char src[] = "Look Here";
	char dest[40] = "Unimaginable";

	char *ps = src + 4;
	char *pd = dest + 6;

	strcat(pd, ps);
	printf("%s", dest);

	return 0;
}
```

In the example above, `ps` points to the 5th character of `src` and `pd` points to the 7th character of `dest`. `strcat` finds the NULL character of `dest` starting from `pd` (i.e. the 7th character of `dest`). This will find the NULL character at the end of `dest` - the same NULL character will be used for any other pointers inside `dest`. Copying starts from the 5th character of `src`, this is what `ps` is pointing to. At the end a NULL character is appended.

**Warning:** When using character pointers, care must be taken so that the source and destination aren't overlapped. Following is an example of ill-formed code which uses `strcat` of overlapped buffer - which causes undefined behaviour:

```C
char dest[40] = "Unimaginable";

char *ps = dest + 6;
char *pd = dest + 4;

/* strcat(pd, ps); */ /* Fatal: pd and ps overlaps - undefined behaviour */
```

