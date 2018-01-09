Let's look at some of the operations that can be performed on a C string without modifying the string(s) involved. To use the functions in this lesson, please make sure to `#include` the header file `string.h`.

## Number of characters in a string - `strlen`

`strlen` returns the number of characters in a C string, _excluding_ the NULL character.

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str[] = "Look Here";

	printf("Number of characters in \'%s\' is %d\n", str, strlen(str));

	return 0;
}

```

## Comparison of different strings - `strcmp`

`strcmp` is used to compare two different C strings. When the strings passed to `strcmp` contains exactly same characters in every index and have exactly same length, it returns 0. For example, `i` will be 0 in the following code:

```
char str1[] = "Look Here";
char str2[] = "Look Here";

int i = strcmp(str1, str2);
```

If the passed parameters aren't same, `strcmp` returns either a positive or a negative integer.

`strcmp` returns a negative integer if the first character that's mismatched between passed parameters has a lower ASCII value in the first string. For example:

```
char str1[] = "Look HerE";
char str2[] = "Look Here";

int i = strcmp(str1, str2);
```

`i` will be a negative number in the above example because the ASCII value of 'E' is lower than the ASCII value of 'e'. This is the first character (index 8) where these two strings differ.

Try the following example, then modify `strX` arrays to your choice and see the result.

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str1[] = "Look HerE";
	char str2[] = "Look Here";
	char str3[] = "Look Here";
	char str4[] = "Look Her";

	printf("%d\n", strcmp(str1, str2));
	printf("%d\n", strcmp(str2, str3));
	printf("%d\n", strcmp(str3, str4));

	return 0;
}

```

## Comparison of different strings upto n-th character - `strncmp`

If you want to compare first n-th characters of two strings, then `strncmp` can be used. Its return value is similar to `strcmp`.

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str1[] = "Look HerE";
	char str2[] = "Look Here";

	printf("%d\", strncmp(str1, str2, 8));
	printf("%d\", strncmp(str1, str2, 9));

	return 0;
}

```

