# 访问类的成员变量和成员函数
#### - 用法1：对象名.成员名
  
```ruby
CRectangle r1,r2;
  r1.w=5;
  r2.lnit(3,4);
```

#### -用法2：指针->成员名

```ruby
CRectangle r1,r2;
CRectangle *p1=&r1;
CRectangle *p2=&r2;
p1->w=5;
p2->lnit(3,4);//lnit作用在p2指向的对象上
```
#### -用法3： 引用名.成员名

```ruby
CRectangle r2;
CRectangle &rr=r2;
rr.w=5;
rr.lnit(3,4);//rr的值改变,r2的值也变
```
# 类成员函数的写法
#### - 写在函数体
#### - 写在函数体外
 
```ruby
在函数体中声明
 返回值类型 函数名(参数1，参数2，...)
    
在函数体外完善
返回值类型 类名：：函数名(参数1，参数2，...)
{
    
}
```
函数的调用仍通过对象，对象的指针，对象的引用
# 类成员的可访问范围
 ## - 关键字
1.  pritvate：指定私有成员，==只能在成员函数内==访问
2.  public：指定公有成员，==可以在任何地方==被访问
3.  protected：指定保护成员
- 关键字的次数和先后顺序不重要
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
