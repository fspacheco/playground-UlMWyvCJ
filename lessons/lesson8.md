If a C string is a one dimensional character array then what's an array of C string looks like? It's a two dimensional character array!

Here is how an array of C string can be initialized:

```C
#define NUMBER_OF_STRING 4
#define MAX_STRING_SIZE 40

char arr[NUMBER_OF_STRING][MAX_STRING_SIZE] =
{ "array of c string",
  "is fun to use",
  "make sure to properly",
  "tell the array size"
};
```

Since all but the highest dimention can be omitted from an array declaration, the above declaration can be reduced to:

```C
#define MAX_STRING_SIZE 40

char arr[][MAX_STRING_SIZE] =
{ "array of c string",
  "is fun to use",
  "make sure to properly",
  "tell the array size"
};
```

But it is a good practice to specify size of both dimensions.

Now each `arr[x]` is a C string and each `arr[x][y]` is a character. You can use any function on `arr[x]` that works on string!

Following example prints all strings in a string array with their lengths.

```C
#define NUMBER_OF_STRING 4
#define MAX_STRING_SIZE 40

char arr[NUMBER_OF_STRING][MAX_STRING_SIZE] =
{ "array of c string",
  "is fun to use",
  "make sure to properly",
  "tell the array size"
};

for (int i = 0; i < NUMBER_OF_STRING; i++)
{
	printf("'%s' has length %d\n", arr[i], strlen(arr[i]));
}
```

Following example reverses all strings in a string array:

```C runnable
#include <stdio.h>
#include <string.h>

#define NUMBER_OF_STRING 4
#define MAX_STRING_SIZE 40

void print_array(const char arr[NUMBER_OF_STRING][MAX_STRING_SIZE])
{
	for (int i = 0; i < NUMBER_OF_STRING; i++)
	{
		printf("'%s' has length %d\n", arr[i], strlen(arr[i]));
	}
}

int main()
{
	char arr[NUMBER_OF_STRING][MAX_STRING_SIZE] =
	{ "array of c string",
	  "is fun to use",
	  "make sure to properly",
	  "tell the array size"
	};

	printf("Before reverse:\n");
	print_array(arr);

	for (int i = 0; i < NUMBER_OF_STRING; i++)
	{
		for (int j = 0, k = strlen(arr[i]) - 1; j < k; j++, k--)
		{
			char temp = arr[i][j];
			arr[i][j] = arr[i][k];
			arr[i][k] = temp;
		}
	}

	printf("\nAfter reverse:\n");
	print_array(arr);

	return 0;
}
```

