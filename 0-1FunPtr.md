# 函数指针
- 把函数的起始位置赋给一个指针，使该指针指向该函数。然后通过指针就可以调用这个函数
- 定义类型： 类型名（*指针变量名）（参数类型1，参数类型2，...）； 类型名为返回值类型。
- 使用方法：用一个原型匹配的函数的名字给一个函数指针赋值。经过赋值后即可以调用
```ruby
#include<stdio.h>
void PrintMin(int a,int b)
{
    if(a<b)
    printf("%d",a);
    else 
    ptintf("%d",b);
}
int main()
{
    void(*pf)(int ,int);
    int x=4,y=5;
    pf=PrintMin;
    pf(x,y);
    return 0;
}
```
- qsort函数
```ruby
void qsort(void *base,int nelem, unsigned int width,int (*pfCompare)(const void*,const void*) );
```
base:待排序数组的起始地址 nelem:待排序数组的元素个数 width：待排序数组的每个元素的大小(字节为单位) pfCompare：比较函数的地址
比较函数格式：
```ruby
int pfCompare(const void*elm1,const void*elem2);
(待比较元素的地址作为参数)
```
编写规则：
如果*elem1应该在*elem2前面，则返回值是负整数；如果哪个在前都行，则返回0；如果*elem1应该在*elem2后面，则返回值是正整数；
例子（从小到大排序）
```ruby
#include<stdio.h>
#include<stdlib.h>
#include<iostream>
using namespace std;
int MyCompare(const void*elem1,const void*elem2)
{
    unsigned int *p1, *p2;
    p1=(unsigned int*) elem1;
    p2=(unsigned int*) elem2;//强制类型转换
    return *p1-*p2;
}
int main()
{
    unsigned int an[5]={0};
    for(int i=0;i<5;i++)
    {
        cin>>an[i];
    }
    qsort(an,5,sizeof(unsigned int),MyCompare);
    for(int i=0;i<5;i++)
    {
        cout<<an[i]<<endl;
    }
    return 0;
}
```
