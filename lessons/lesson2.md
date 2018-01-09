Let's look at some of the operations that can be performed on a C string without modifying it. To use the functions in this lesson, please make sure to `#include` the header file `string.h`.

# Number of characters in a string - `strlen`

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

