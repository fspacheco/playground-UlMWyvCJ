# Split a string into tokens - `strtok`

In this lesson we'll learn how to split a string into several _tokens_ using `strtok` function. To split a string we need delimiters - delimiters are characters which will be used to split the string.

Suppose, we've the following string and we want to extract the individual words.

```C
char str[] = "strtok needs to be called several times to split a string";
```

The words are separated by space. So space will be our delimiter.

```C
char delim[] = " ";
```

`strtok` accepts two strings - the first one is the string to split, the second one is a string containing all delimiters. In this case there is only one delimiter. `strtok` returns a pointer to the character of next token. So the first time it is called, it will point to the first word.

```C
char *ptr = strtok(str, delim);
```

```
strtok needs to be called several times to split a string
^
ptr points here
```

But there is another thing. `strtok` modifies the original string. It puts NULL characters ('\0') at the delimiter position after every call to `strtok` so that tokens can be tracked. `strtok` also internally remembers the next token's starting position. So after the first call to `strtok`, the `str`, `ptr` and next token position looks like as follows:

```
strtok\0needs to be called several times to split a string
^       ^
|       next token
|
ptr points here
```

In the next call to `strtok`, the first parameter needs to be NULL so that `strtok` starts splitting the string from the next token's starting position it remembers.

```C
ptr = strtok(NULL, delim);
```

`strtok` returns NULL when there is no more tokens, i.e., the whole string is split. This can be utilized to know when to stop calling `strtok`. Putting it all together in complete example below.

```C runnable
#include <stdio.h>
#include <string.h>

int main()
{
	char str[] = "strtok needs to be called several times to split a string";
	int init_size = strlen(str);
	char delim[] = " ";

	char *ptr = strtok(str, delim);

	while(ptr != NULL)
	{
		printf("'%s'\n", ptr);
		ptr = strtok(NULL, delim);
	}

	/* This loop will show that there are zeroes in the str after tokenizing */
	for (int i = 0; i < init_size; i++)
	{
		printf("%d ", str[i]); /* Convert the character to integer, in this case
							   the character's ASCII equivalent */
	}
	printf("\n");

	return 0;
}
```

**Warning:** Because `strtok` modifies original string, character pointer to read-only string shouldn't be passed to `strtok`. The following examples will trigger undefined behaviour because the first parameter to `strtok` is read-only string:

```C
char *str = "strtok needs to be called several times to split a string";
char *ptr = strtok(str, delim);
```

```C
char *ptr = strtok("strtok needs to be called several times to split a string", delim);
```

If you don't want the original string to be modified, create a copy of the original string using `strcpy` and pass that copy to `strtok`.

