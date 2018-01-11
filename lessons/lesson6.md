We're going to do some amazing thing from this lesson. Let's see how searching works.

# Search for a character in a string - `strchr` & `strrchr`

The `strchr` function returns the first occurrence of a character within a string. The `strrchr` returns the last occurrence of a character within a string. They return a character pointer to the character found, or NULL pointer if the character is not found. Using these functions, lets write a program that output the index of first and last occurrence of all characters in alphabet (a-z, small letters only).

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
