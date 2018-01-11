Examples in this lesson modifies existing string.

# Appending one string at the end of another - `strcat`

The `strcat` function is used to concatenate one string (source) at the end of another string (destination). It does the following:

1. Takes the destination string.
2. Finds the NULL character.
3. Copies the source string starting at the location of the NULL character of destination string.
4. Appends a NULL character to the destination string when all characters of the source string are copied to the destination string.

Here is an example:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char src[] = "Look Here";
	char dest[DEST_SIZE] = "Unimaginable";

	strcat(dest, src);
	printf(dest);

	return 0;
}
```

Notice how it works. When `dest` is initialized with `char dest[DEST_SIZE] = "Unimaginable";` there is a NULL character at the end. That's the starting point for the source string to be copied. When all characters of source string are copied to `dest`, a NULL character is appended.

**Warning:** The destination character array must be large enough to hold all characters of source, all characters of destination and a NULL character. Following ill-formed code triggers undefined behaviour:

```C
char src[] = "Look Here";
char dest[] = "Unimaginable";

/* strcat(dest, src); */ /* Fatal: dest doesn't have enough spaces to hold
                         all characters of dest
                         all chracters of src
                         a NULL character */
printf(dest);
```

**Warning:** The destination character array must be initialized with C string before passing it to `strcat`. In other words, the destination character array must have at least 1 location which has a NULL character. Following is an ill-formed code and shouldn't be practiced:

```C
#define DEST_SIZE 40

char dest[DEST_SIZE];

/* strcat(dest, "Look Here"); */ /* Fatal: dest is not initialized
                                 - no guarantee about a NULL character 
                                 - undefined behaviour */
/* printf(dest); */ /* Fatal: dest isn't initialized - results in undefined behaviour */
```

At minimum the destination array could be initialized as empty string (only the NULL character) and after that `strcat` can be used:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char dest[DEST_SIZE] = "";

	strcat(dest, "Look Here");
	printf(dest);

	return 0;
}

```

If the destination character array is declared at global scope, then all elements of the array are initialized to 0 automatically by C. Since a 0 is equivalent to NULL character, an array declared globally can be directly passed to `strcat`:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

char dest[DEST_SIZE];

int main()
{
	strcat(dest, "Look Here");
	printf(dest);

	return 0;
}

```

Character pointers can be used in `strcat`:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char src[] = "Look Here";
	char dest[DEST_SIZE] = "Unimaginable";

	char *ps = src + 4;
	char *pd = dest + 6;

	strcat(pd, ps);
	printf(dest);

	return 0;
}
```

In the example above, `ps` points to the 5th character of `src` and `pd` points to the 7th character of `dest`. `strcat` finds the NULL character of `dest` starting from `pd` (i.e. the 7th character of `dest`). This will find the NULL character at the end of `dest` - the same NULL character will be used for any other pointers inside `dest`. Copying starts from the 5th character of `src`, this is what `ps` is pointing to. At the end a NULL character is appended.

**Warning:** When using character pointers, care must be taken so that the source and destination aren't overlapped. Following is an example of ill-formed code which uses `strcat` of overlapped buffer - which causes undefined behaviour:

```C
#define DEST_SIZE 40

char dest[DEST_SIZE] = "Unimaginable";

char *ps = dest + 6;
char *pd = dest + 4;

/* strcat(pd, ps); */ /* Fatal: pd and ps overlaps - undefined behaviour */
```

# String concatenation upto n characters - `strncat`

The `strncat` function is used to append at most n characters from source string to destination string. Here is an example:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char src[] = "Look Here";
	char dest[DEST_SIZE] = "Unimaginable";

	strncat(dest, src, 4);
	printf(dest);

	return 0;
}
```

The example above will append first 4 characters from `src` at the end of `dest` (i.e. starting from the NULL character of `dest`) and appends a NULL character in the end.

**Warning:** The destination character array must be large enough to hold all characters of destination, n characters of source and a NULL character. Following is an example of an ill-formed code which violates this rule:

```
#define DEST_SIZE 4

char src[] = "Look Here";
char dest[DEST_SIZE] = "A";

/* strncat(dest, src, 4); */ /* Fatal: dest doesn't have enough space for
                             all characters of dest
                             4 characters of src
                             a NULL character */
printf(dest);
```

Character pointers can be used to the parameters of `strncat`:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char src[] = "Look Here";
	char dest[DEST_SIZE] = "Unimaginable";

	char *ps = src + 4;

	strncat(dest, ps, 5);
	printf(dest);

	return 0;
}
```

In the example above, `ps` points to the 5th character of `src` (that's the space). The call to `strncat` finds the NULL character of `dest`, appends 5 characters starting from `ps` and finally appends a NULL character.

**Warning:** When using character pointers be careful to the fact that the source and the destination cannot be overlapped. If the source and destination overlaps, this will trigger undefined behaviour. Following is such an example of bad coding:

```C
#define DEST_SIZE 40

char dest[DEST_SIZE] = "Unimaginable";

char *sp = dest + 5;
char *dp = dest + 8;

/* strncat(dp, sp, 5); */ /* Fatal: source and destination aren't allowed to overlap */
```

If the number of characters to copy is more than the characters in the source string, `strncat` will stop appending when it will encounter the NULL character in source. In the example below `strncat` stops concatenation as soon as it reaches the NULL character of `src`:

```C
#define DEST_SIZE 40

char src[] = "Look Here";
char dest[DEST_SIZE] = "Unimaginable";

char *ps = src + 4;

strncat(dest, ps, 10); /* The third parameter is 10, but there are 5 characters before the NULL character from ps */
printf(dest); /* Output: Unimaginable Here */
```

