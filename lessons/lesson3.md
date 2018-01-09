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

The destination character array **must be large enough** to hold all characters in source character array, plus a NULL character. Following code snippet will result in undefined behaviour:

```
char src[] = "Look Here";
char dest[4] = "A";

strcpy(dest, src); /* Fatal: dest doesn't have enough space to hold all characters of src */
```
