Examples in this lesson modify a string/character array.

## Copying one string to another - `strcpy`

`strcpy` can be used to copy one string to another. Remember that C strings are character arrays. You must pass character array, or pointer to character array to this function where string will be copied.

The following example will overwrite the contents of `dest` with the content of `src`:

```
char src[] = "Look Here";
char dest[40] = "Unimaginable";

strcpy(dest, src);

printf("%s", dest); /* Output: Look Here */
```

The destination character array is the first parameter to `strcpy`. The source character array is the second parameter to `strcpy`.

The destination character array **must be large enough** to hold all characters in source character array, plus a NULL character. If the source array has 100 characters, the destination array must be at least 101 character long. Following code snippet will result in undefined behaviour:

```
char src[] = "Look Here";
char dest[4] = "A";

strcpy(dest, src); /* Fatal: dest doesn't have enough space to hold all characters of src */
```

The destination character array doesn't have to initialized. It can be left uninitialized and can be passed to `strcpy`. Still, it must have enough space to hold the source array and a NULL character.

```
char src[] = "Look Here";
char dest[40];

strcpy(dest, src);
printf("%s", dest); /* Output: Look Here */
```

Also possible:
```
char dest[40];

strcpy(dest, "Look Here");
printf("%s", dest); /* Output: Look Here */
```

Character pointers can also be passed as parameters of `strcpy`.

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char src[] = "Look Here";
	char dest[40] = "Unimaginable";

	char *p = dest + 5;

	strcpy(p, src);
	printf("%s", dest);

	return 0;
}

```

What happens in the example above is that `p` points to the 6th character of `dest`. When `p` is passed as the first parameter of `strcpy`, it becomes the first character to be overwritten by the function. So `src` gets copied starting at the 6th character of `dest`.

**Warning**: Care must be taken when passing character pointers to `strcpy`. The source and destination aren't allowed to overlap. For example, the following is forbidden:

```
char dest[40] = "Unimaginable";

char *sp = dest + 5;
char *dp = dest + 8;

strcpy(dp, sp);
```

In the example above, `sp` points to the 6th character of `dest` and `dp` points to the 9th character of `dest`. Both of them share the same array (`dest`). This is not allowed and executing code like this may result unexpected results.