---
title: C语言任意类型数组排序
date: 2021-01-31 21:22:26
categories: C
---

### 前言

众所周知，C语言里面有一个`qsort()`函数，底层是结合了回调函数的快排，功能很强大，可以实现任意类型的数组排序，今天我们就来复现一下。

目标：实现一个`sortArray()`函数，实现任意类型的数组排序。

### 回调函数

所谓回调函数，本质上就是函数指针做函数参数。

C语言嘛，万物皆可指针，当然函数也不例外。

```C
#include <stdio.h>

void func(void)
{
    printf("Hello World\n");
}

int main(void)
{
    printf("%d",func);
    return 0;
}
```

以上程序执行之后输出的不是`Hello World`，而是类似`4199760`这样的一串数字。实际上这就是函数入口地址，只不过是十进制显示的。

要实现**任意类型**的排序，那么待排序的元素类型就不确定，有可能是整数，有可能是小数，还有可能是结构体，我们不可能确定待排序元素的类型。C又没有面向对象，解决办法就是抽象出两个层：**服务层**和**用户层**。

在服务层写好排序算法，然后抽象出一个涉及具体元素的函数，交给用户去实现，因为只有用户知道这个类型是什么。服务层只是在底层提供一个统一的接口，配合用户层利用回调函数完成整个功能。

用户层就是实现具体的回调函数。用过`qsort()`函数的同学应该都明白，你得写一个`int compar(const void *, const void *)`这样的函数然后把函数名当作参数传入`qsort()`，这里就不赘述了（懒……

### 排序算法

如果从排序效率来说的话，当然是快排高咯，但是本文重点是**任意类型**的数组排序，所以就只演示一下用冒泡排序（用快排的话指针满天飞太吓人了……）

冒泡排序没啥好说的，应该都会。涉及到具体的元素，比如比较两个元素大小只能用回调函数了，但是交换任意类型的两个元素呢？

虽然也可以再用一个回调函数，但是原则是：**如果能自己做到就不要麻烦用户**。

那么，有没有什么办法不用回调函数实现任意类型的元素互换呢？如果是`int`，直接定义一个临时变量然后交换就好了，可是现在我们面临的是任意类型……嗯……有了！我们有元素首地址`eleAddr`，有每个元素的大小`eleSize`，那么直接互换内存不就好了？对！用`memcpy()`函数，bingo！

于是服务层的代码如下：

```C
void sortArray(void *arr, int eleSize, int len, int (*myCmp)(const void *, const void *))
{
    char *temp = malloc(eleSize);
    for (int i = 0; i < len - 1; i++)
    {
        int isSwapped = 0;
        for (int j = 0; j < len - i - 1; j++)
        {
            char *eleAddr = (char *)arr + eleSize * j;
            char *eleAddrPlus = (char *)arr + eleSize * (j + 1);
            if (myCmp(eleAddrPlus, eleAddr))
            {
                // 利用memcpy()交换元素
                memcpy(temp, eleAddrPlus, eleSize);
                memcpy(eleAddrPlus, eleAddr, eleSize);
                memcpy(eleAddr, temp, eleSize);
                isSwapped = 1;
            }
        }
        if (isSwapped == 0)
        {
            break;
        }
    }
    free(temp);
    temp = NULL;
}
```

### 整数数组排序

然后用户层的回调函数实现起来就很简单了：

```c
int myCmpInt(const void *a, const void *b)
{
    const int *p1 = a;
    const int *p2 = b;
    return *p1 > *p2; // ">" 降序排列
}

int main(void)
{
    int arrInt[] = {2, 5, 7, 5, 4, 3, 8, 21, 9, 0, 99};

    /* 动态获取长度 */
    int lenArrInt = sizeof(arrInt) / sizeof(int);
    sortArray(arrInt, sizeof(int), lenArrInt, myCmpInt);
    for (int i = 0; i < lenArrInt; i++)
    {
        printf("%d ", arrInt[i]);
    }
    printf("\n");

    return 0;
}
```

输出结果是：

```
99 21 9 8 7 5 5 4 3 2 0
```

### 结构体数组排序

直接内存互换的好处就在这里：无论是什么类型，直接在最底层执行内存互换，还有什么换不了的？

```c
struct Person
{
    char name[64];
    int age;
};

int myCmpPersonAge(const void *a, const void *b)
{
    const struct Person *p1 = a;
    const struct Person *p2 = b;
    return p1->age < p2->age;
}

int myCmpPersonName(const void *a, const void *b)
{
    const struct Person *p1 = a;
    const struct Person *p2 = b;
    return strcmp(p1->name, p2->name) < 0;
}

int main(void)
{
    // int arrInt[] = {2, 5, 7, 5, 4, 3, 8, 21, 9, 0, 99};
    struct Person arrPerson[] = {
        {"Alice", 18},
        {"Sakura", 19},
        {"Homura", 20},
        {"Mei", 17},
        {"Yuzu", 18},
    };

    /* 动态获取长度 */
    // int lenArrInt = sizeof(arrInt) / sizeof(int);
    // sortArray(arrInt, sizeof(int), lenArrInt, myCmpInt);
    // for (int i = 0; i < lenArrInt; i++)
    // {
    //     printf("%d ", arrInt[i]);
    // }
    // printf("\n");

    /* 动态获取长度 */
    int lenArrPerson = sizeof(arrPerson) / sizeof(struct Person);
    /* 根据结构体元素的年龄排序 */
    printf("Order by Age-----------\n");
    sortArray(arrPerson, sizeof(struct Person), lenArrPerson, myCmpPersonAge);
    for (int i = 0; i < lenArrPerson; i++)
    {
        printf("Name: %s\tAge: %d\n", arrPerson[i].name, arrPerson[i].age);
    }
    /* 根据结构体元素的姓名排序 */
    printf("Order by Name----------\n");
    sortArray(arrPerson, sizeof(struct Person), lenArrPerson, myCmpPersonName);
    for (int i = 0; i < lenArrPerson; i++)
    {
        printf("Name: %s\tAge: %d\n", arrPerson[i].name, arrPerson[i].age);
    }

    return 0;
}
```

输出结果是：

```
Order by Age-----------
Name: Mei       Age: 17
Name: Alice     Age: 18
Name: Yuzu      Age: 18
Name: Sakura    Age: 19
Name: Homura    Age: 20
Order by Name----------
Name: Alice     Age: 18
Name: Homura    Age: 20
Name: Mei       Age: 17
Name: Sakura    Age: 19
Name: Yuzu      Age: 18
```

以上。

---

