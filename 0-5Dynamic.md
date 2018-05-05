# 动态内存分配
#### -   用new运算符实现动态内存分配
1. 分配一个变量
   P=new T(T为类型名，P是==(*T)==的指针，动态分配出一片大小为sizeof(T)字节的内存空间，并将该内存的起始地址赋给P
```ruby
int *pn;
pn=new int;
*pn=5;
```

2. 分配一个数组
   P=new T[N];  
T为类型名 P为==T*==的指针N为要分配的数组元素的个数，可以使整型表达式
动态分配出一片大小为N*sizeof(T)的内存空间，并将该内存空间的起始地址赋给P
```ruby
int *pn;
int i=5;
pn=new int[i*20];
pn[0]=20;
pn[100]=30;//编译能通过，执行时会有问题，大小为100，最大下标为99
```

#### 用new运算符实现动态内存分配
new运算符的返回值类型： new T;new T[N];返回值都是==T*==
#### - 用delete运算符释放动态分配的内存

```ruby
delete 指针;//该指针指向new出来的空间
int *p=new int;
*p=5;
delete p;
delete p;//异常，一片空间不能被释放两次
```
- #### delete数组

```ruby
delete 指针;//指针指向new出来的数组

int *p=new int [20];
p[0]=1;
delete []p;
```
