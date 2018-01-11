We're going to do some amazing thing from this lesson. Let's see how searching works.

# Search for a character in a string - `strchr` & `strrchr`

The `strchr` function returns the first occurrence of a character within a string. The `strrchr` returns the last occurrence of a character within a string. They return a character pointer to the character found, or NULL pointer if the character is not found. Using these functions, lets write a program that output the index of first and last occurrence of all lower case characters in a string.

We define the string to be searched.

```C
char str[] = "finding first and last occurrence of a character is amazing";
```

We'll loop through all lower case characters. Let's define a character array for that and write a loop.

```C
char alpha[] = "abcdefghijklmnopqrstuvwxyz";

for (int i = 0; i < strlen(alpha); i++)
{
}
```

Both `strchr` and `strrchr` returns a pointer to the character where the occurrence of the sought character is found. Say, the string to be searched is "abcd" and the character to be searched for is 'b'. Then a pointer to character 'b' within the string is returned. If the character is not found then `NULL` is returned.

We declare two character pointers to hold the returned values from the functions. Remember, we search for `alpha[i]` within `str`.

```C
char *position_ptr = strchr(str, alpha[i]);
char *r_position_ptr = strrchr(str, alpha[i]);
```

These character pointers are simply the address of the character found within the array. If we subtract the first address from this address, then we'll find the index of the character. The starting address of the array can be accessed by the array name. So the index is calculated as follows:

```C
int position = position_ptr - str;
int r_position = r_position_ptr - str;
```

There is a problem in the code above. The character pointers can be NULL - in case the character is not found in the string. We can define that if a character is not found within the string, then the character's index is `-1` (because `-1` is an invalid index, we can use it for this purpose). Considering NULL pointer, the positions are redefined as:

```C
int position = (position_ptr == NULL ? -1 : position_ptr - str);
int r_position = (r_position_ptr == NULL ? -1 : r_position_ptr - str);
```

So we've everything now. We can simply output these positions. Here is a complete example:

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str[] = "finding first and last occurrence of a character is amazing";
	char alpha[] = "abcdefghijklmnopqrstuvwxyz";

	printf("String to search: %s\n", str);
	printf("Length of string: %d\n", strlen(str));
	printf("Char: first last\n");

	for (int i = 0; i < strlen(alpha); i++)
	{
		char *position_ptr = strchr(str, alpha[i]);
		char *r_position_ptr = strrchr(str, alpha[i]);

		int position = (position_ptr == NULL ? -1 : position_ptr - str);
		int r_position = (r_position_ptr == NULL ? -1 : r_position_ptr - str);

		printf("%4c: %4d %4d\n", alpha[i], position, r_position);
	}

	return 0;
}

```

# Search for string inside another string - `strstr`

A substring is a contiguous elements of a string. As an example, "ea", "ch" etc are substrings of "teacher"; but "cer" isn't. The function `strstr` returns the first occurrence of a string in another string. This means that `strstr` can be used to detect whether a string contains another string. In other words, whether a string is a substring of another string.

`strstr` returns the first occurrence of the substring in another string in the form of a character pointer pointing to the first character of the match. Consider the following example:

```C
char str[] = "teacher teach tea";
char *ptr = strstr(str, "ac");
```

 `ptr` will point to the character 'a' of first "ac" in `str`:
 
```
teacher teach tea
  ^
  ptr points here
```

However, if the string is not found, `strstr` returns NULL pointer. Using the NULL check, we can verify whether a string contains another string. Here is a complete example:

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str[] = "teacher teach tea";
	char search[] = "ac";
	char *ptr = strstr(str, search);

	if (ptr != NULL) /* Substring found */
	{
		printf("'%s' contains '%s'\n", str, search);
	}
	else /* Substring not found */
	{
		printf("'%s' doesn't contain '%s'\n", str, search);
	}

	return 0;
}
```

# Search for occurrence of any character in a string - `strpbrk`

Using `strchr` one can find if a string contain a single character. What if someone wants to find if a string contains any character from a group of characters? That's what `strpbrk` does.

You provide two strings to `strpbrk`. If any character from second string is found in the first string, `strpbrk` will return a character pointer to the first occurrence. Let's say, you've a string like:

```C
char str[] = "finding digits where there could be digit 5236 is amazing";
```

You want to know if `str` contains any digits.  So you define a `digits` array:

```C
char digits[] = "0123456789";
```

Plug them in to `strpbrk`:

```C
char *ptr = strpbrk(str, digits);
```

Because `str` contains character from `digits`, `ptr` will point to its first occurrence:

```
finding digits where there could be digit 5236 is amazing
                                          ^
                                          ptr points here
```

`ptr` will be NULL pointer if no character from second parameter is present in the first parameter. Using NULL check we can verify whether any character from second parameter is present in first parameter. Here is a complete example:

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str[] = "finding digits where there could be digit 5236 is amazing";
	char digits[] = "0123456789";
	char *ptr = strpbrk(str, digits);

	if (ptr != NULL) /* Expected character is found */
	{
		printf("'%s' contains at least one character from '%s'\n", str, digits);
	}
	else /* Expected character isn't found */
	{
		printf("'%s' doesn't contain any character from '%s'\n", str, digits);
	}

	return 0;
}

```

