There are many Standard C library functions which can be used devastatingly! If the programmers are not careful, they can leave bugs in their program deep inside. These bugs are very difficult to trace as they produce very unexpected behaviour. Many of the functions that deal with strings fall into this category. In recent revisions of the standard many alternative **safe** functions are introduced. These safe functions are recommended to use. However, they are not strictly maintained by all compilers as the compiler developers are not forced to include all safe functions in their compiler package.

This tutorial will highlight safe variants of the functions first. Then the **unsafe** function that does the same thing will be introduced. In case the safe variants haven't come to the compiler you use, you can proceed with the unsafe functions - please be careful. Also remember that the unsafe variants promote bad programming practice.

The **safe** variants will be marked with ![Safe variant](../images/green-c-small.png)

The **unsafe** variants will be marked with ![Unafe variant](../images/red-c.png)
