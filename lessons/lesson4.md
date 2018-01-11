Examples in this lesson modify a string/character array.

# Copying one string to another - `strcpy`

`strcpy` can be used to copy one string to another. Remember that C strings are character arrays. You must pass character array, or pointer to character array to this function where string will be copied.

The following example will overwrite the contents of `dest` with the content of `src`:

```C
#define DEST_SIZE 40

char src[] = "Look Here";
char dest[DEST_SIZE] = "Unimaginable";

strcpy(dest, src);
printf(dest); /* Output: Look Here */
```

The destination character array is the first parameter to `strcpy`. The source character array is the second parameter to `strcpy`. The terminating NULL character is automatically appended at the end of the copy.

**Warning:** The destination character array must be large enough to hold all characters in source character array, plus a NULL character. If the source array has 100 characters, the destination array must be at least 101 character long. Following code snippet will result in undefined behaviour:

```C
char src[] = "Look Here";
char dest[4] = "A";

/* strcpy(dest, src); */ /* Fatal: dest doesn't have enough space to hold all characters of src plus a NULL character */
```

The destination character array doesn't have to initialized. It can be left uninitialized and can be passed to `strcpy`. Still, it must have enough space to hold the source array and a NULL character.

```C
#define DEST_SIZE 40

char src[] = "Look Here";
char dest[DEST_SIZE];

strcpy(dest, src);
printf(dest); /* Output: Look Here */
```

Also possible:
```C
#define DEST_SIZE 40

char dest[DEST_SIZE];

strcpy(dest, "Look Here");
printf(dest); /* Output: Look Here */
```

Character pointers can also be passed as parameters of `strcpy`.

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char src[] = "Look Here";
	char dest[DEST_SIZE] = "Unimaginable";

	char *p = dest + 5;

	strcpy(p, src);
	printf(dest);

	return 0;
}

```

What happens in the example above is that `p` points to the 6th character of `dest`. When `p` is passed as the first parameter of `strcpy`, it becomes the first character to be overwritten by the function. So `src` gets copied starting at the 6th character of `dest` leaving first 5 characters untouched.

Of course, the second parameter could also be pointer to character:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 40

int main()
{
	char src[] = "Look Here";
	char dest[DEST_SIZE] = "Unimaginable";

	char *ps = src + 4;
	char *pd = dest + strlen(dest);

	strcpy(pd, ps);
	printf(dest);

	return 0;
}
```

In the example above `ps` points to the space character of `src`. `pd` points to the NULL character of `dest`. So the call to `strcpy` overwrites the NULL character of `dest` with space character of `src`, followed by other characters of `src`, finally a NULL character is appended.

**Warning**: Care must be taken when passing character pointers to `strcpy`. The source and destination aren't allowed to overlap. For example, the following is forbidden:

```C
#define DEST_SIZE 40

char dest[DEST_SIZE] = "Unimaginable";

char *sp = dest + 5;
char *dp = dest + 8;

/* strcpy(dp, sp); */ /* Fatal: source and destination aren't allowed to overlap */
```

In the example above, `sp` points to the 6th character of `dest` and `dp` points to the 9th character of `dest`. Both of them share the same array (`dest`). This is not allowed and executing code like this may produce unexpected results.

# Copying first n characters from one string to another - `strncpy`

`strncpy` is used to copy first several characters from source string to destination string. It doesn't append any NULL character when the copying finishes.

In the following example, the first 5 characters are copied. No NULL character is appended.

```C
#define DEST_SIZE 40

char src[]    = "Look Here";
char dest[DEST_SIZE] = "Unimaginable";

strncpy(dest, src, 5);
printf(dest); /* Output: Look ginable */
```

**Warning:** Care must be taken when using `strncpy` to make sure that strings are NULL terminated. Following is an example of an ill-formed code which doesn't take NULL character into account:

```C
#define DEST_SIZE 9

char src[]  = "Look Here"; /* src has 9 + 1 = 10 characters */
char dest[DEST_SIZE]; /* dest can only hold 9 characters */

strncpy(dest, src, 9); /* First 9 characters are copied to dest, where is the NULL character? */
/* printf(dest); */ /* Fatal: undefined behaviour - dest doesn't have a NULL character */
```

But it's fine if each characters are accessed individually:

```C runnable
#include <stdio.h>
#include <string.h>

#define DEST_SIZE 9

int main()
{
	char src[] = "Look Here"; /* src has 9 + 1 = 10 characters */
	char dest[DEST_SIZE]; /* dest can only hold 9 characters */

	strncpy(dest, src, 9); /* First 9 characters are copied to dest, where is the NULL character? */
	/* printf("%s", dest); */ /* Fatal: undefined behaviour - dest doesn't have a NULL character */

    /* Print out the string by accessing each character individually */
	for (int i = 0; i < DEST_SIZE; i++)
	{
		printf("%c", dest[i]);
	}

	return 0;
}
```

If the number of characters to copy is more than the characters in the source string, `strncpy` will stop copying when it will encounter the NULL character in source. In the example below `strncpy` stops copying as soon as it reaches the NULL character of `src`:

```C
#define DEST_SIZE 40

char src[] = "Look Here";
char dest[DEST_SIZE] = "Unimaginable";

char *ps = src + 3;

strncpy(dest, ps, 10); /* The third parameter is 10, but there are 6 characters before the NULL character from ps */
printf(dest); /* Output: k Here */
```

