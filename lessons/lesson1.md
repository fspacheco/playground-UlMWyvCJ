Uma string em C é um vetor (_array_) de caracteres seguido por caractere nulo (NULL: \0), que marca o fim da string. Um caractere isolado em C é representado entre apóstrofos (aspas simples: '). Já uma string, é representada entre aspas ("). A string "Olhe Aqui" ficaria assim na memória:

```
-----------------------------------------
| O | l | h | e |  | A | q | u | i | \0 |
-----------------------------------------
```

É um array de 10 caracteres.

Neste tutorial, só caracteres de um byte são considerados. O mesmo conceito pode ser expandido para caracteres multibytes, que são importantes para representar letras com acentos e outras línguas além do inglês.

# How to initialize a variable with C string

Existem diferentes formas de inicializar uma variável para acessar uma string.

```C
char *char_ptr = "Olhe Aqui";
```

This initializes `char_ptr` to point to the first character of the **read-only** string `"Look Here"`. Yes, a C string initialized through a character pointer cannot be modified. When a C string is initialized this way, trying to modify any character pointed to by `char_ptr` is **undefined behaviour**. An undefined behaviour means that when a compiler encounters anything that triggers undefined behaviour, it is allowed to do anything it seems appropriate. For maximum portability of your program, make sure to avoid any undefined behaviour.

For example, the following C code crashes when compiled in Visual C++ 2017 when the commented out line is un-commented and the code is executed:

```C runnable
#include <stdio.h>

int main()
{
	char *char_ptr = "Look Here";

    /* Warning: uncommenting the following line will trigger undefined behaviour */
	/* char_ptr[4] = '_'; */
	printf(char_ptr);

	return 0;
}

```

Uma forma mais conveniente de inicializar uma string é através de um vetor de caracteres:

```C
char char_array[] = "Olhe Aqui";
```

Isto é o mesmo que inicializar assim:

```C
char char_array[] = { 'O', 'l', 'h', 'e', ' ', 'A', 'q', 'u', 'i', '\0' };
```

Mas a primeira forma é mais intuitiva. Observe que quando inicializado como `char char_array[] = "Olhe Aqui";`, o caractere NULL é incluído automaticamente.

Qualquer caractere no vetor pode ser modificado:

```C runnable
#include <stdio.h>

int main()
{
	char char_array[] = "Olhe Aqui";

	char_array[4] = '_';
	printf(char_array);

	return 0;
}

```

Assim como qualquer outro vetor, você pode informar o tamanho dentro de `[]` na declaração:

```C
char char_array[15] = "Olhe Aqui";
```

Tenha certeza de que o tamanho que você informa dentro de `[]` é grande o suficiente para guardar todos os caracteres da string mais o caractere NULL. Neste exemplo, os índices de 0 a 9 serão inicializados com os caracteres do texto e o NULL. Os outros índices (10 a 14) serão incializados com 0 (mesmo que o caractere NULL quando convertido para `char`). Na memória, o vetor fica assim:

```
------------------------------------------------------------------
| O | l | h | e |  | A | q | u | i | \0 | \0 | \0 | \0 | \0 | \0 |
------------------------------------------------------------------
  0   1   2   3   4  5   6   7   8   9    10   11   12   13   14
```

Uma forma melhor de declarar um vetor de caracteres (na verdade, qualquer vetor) é definir uma constante para o tamanho e usá-la na declaração do vetor:

```C
#define ARRAY_SIZE 15
char char_array[ARRAY_SIZE] = "Olhe Aqui";
```

