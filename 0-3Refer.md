# 引用
- 某个变量的引用，等价于这个变量。对引用进行操作时，原来的变量也会进行相应的改变。
- ==类型名&引用名=某变量名；=
```ruby
int n=7;
int &r=n;
r=4;
cout<<r;//输出4
cout<<n;//输出4
n=5;
cout<<r;//输出5
```
即改变是共同的，改变初始变量和引用中的任一，两者的值都会变。

- 注意点：1.定义引用时，一定要将其初始化成引用某个==变量==2.初始化后就一直引用该变量，不会再引用其他变量，从一而终啊~3.只能引用变量，不能引用常量。
- 使用1
```ruby
void swap(int a,int b)
{
    int tmp;
    tmp=a;
    a=b;
    b=tmp;
}
int n1,n2;
swap(n1,n2);//n1,n2的值不会被交换，只是值传递

void swap(int &a,int &b)
{
    int tmp;
    tmp=a;
    a=b;
    b=tmp;
}
int n1,n2;
swap(n1,n2);//n1,n2值被修改
```
- 使用2(引用作为函数返回值)
```ruby
int n=4;
int &SetValue()
{
    return n;//返回值引用了n
}
int main()
{
    SetValue()=40;//对函数进行赋值相当于对n进行赋值
    cout<<n;
    return 0;
}
```
- 使用3(常引用)
定义引用时，前面加const关键字。
```ruby
int n;
const int &r=n;
```
r的类型是 const int &

- 特点：不能通过常引用去修改其引用内容
```ruby
int n=100;
const int &r=n;
r=200//错误
n=300//正确，引用的内容可以被修改
```

- 常引用(const &T)和非常引用(T &)是不同的类型。T&型的引用或T类型的变量可以用来初始化const T&类型的引用。const T类型的常变量和const T&类型的引用不能用来初始化T＆类型的引用，除非进行强制类型转换。
