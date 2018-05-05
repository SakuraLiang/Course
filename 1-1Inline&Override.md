# 内联成员函数和重载函数
#### - 内联成员函数
- 定义方式：
1. inline +成员函数
2. 整个函数体出现在类定义内部

```ruby
class B
{
    inline void func1();
    void func2()
  {
    
  };
};
void B::func1(){}
```
#### - 重载成员函数
1.成员函数带缺省参数，调用时首先匹配有参数的，如果没有参数，就是却缺省参数。使用缺省参数时要注意避免函数重载的二义性。 

```ruby
class Location{
    private:
    int x,y;
    public:
    void init(int x=0,int y=0);
    void valueX(int val=0)
    {
       x=val; 
    }
    int valueX()
    {
        return x;
    }
};
Location A;
A.valueX();//error,编译器无法判断调用哪个valueX函数
```
