# 函数模板、类模板
- 函数模板
  
```ruby
 void Swap(int &x,int &y)
 {
     int temp;
     temp=x;
     x=y;
     y=temp;
 }
 
 void Swap(double &x,double &y)
 {
     double temp;
     temp=x;
     x=y;
     y=temp;
 }
 
 template <class T>
 void Swap(T &x, T &y)
 {
     T temp;
     temp=x;
     x=y;
     y=temp;
 }

```
1. 调用函数时，才会根据调用函数的实参生成具体函数。
2. 函数模板也可以重载，只要形参表不同即可。
3. C++编译器遵循规则：1.先找参数完全匹配的普通函数而非模板函数。2.寻找参数完全匹配的模板函数。3.寻找实参经过自动类型转换后能够匹配的普通函数。
4. 可以使用多个类型参数来避免函数二义性

- 类模版
1. 在定义类的时候给它一个或多个参数，这些参数表示不同的类型。在调用类模版时，指定参数，由编译器系统根据参数提供的数据类型自动产生相应的模板类。

```ruby
template<类型参数表（若干个）>
class 类模板名
{
  成员函数和成员变量
};

类型参数表：
class 类型参数1，class类型参数2，...
```

```ruby
template <class T1,class T2>
class Pair
{
    T1 key;
    T2 value;
    Pair(T1 k,T2 v):key(k),value(v){
};//构造函数
bool operator < (const Pair<t1,T2>& p) const;
};
template<class T1,class T2>
bool Pair<T1, T2>::operator <(const Pair<T1,T2>&p) const
{
    return key<p.key;
}
//在类模板外定义时，
template <型参数表>
返回值类型 类模板名<类型参数名列表>：：成员函数名（参数表）
{
    
}
```

2. 编译器自动用具体的数据类型替换模板中的类型参数，生成模板类的代码。为类型参数指定的数据类型不同，得到的模板类不同。
3. 同一个类模板的两个模板类是不兼容的。
```ruby
Pair<string,int> *p;
Pair<string,double>a;
p=&a;//wrong

```
# 函数模板作为类模板成员
