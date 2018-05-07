# 继承和派生
### 概念
- 继承：在定义一个新的类B时，如果该类与某个已有的类A相似(指的是B拥有A的全部特点)，那么就可以把A作为一个基类，而把B作为一个派生类。
- 派生类是通过对基类进行修改(定义同名的函数，执行不同的操作)和扩充(扩充新的成员变量和成员函数)得到的
- 派生类一经定义后，可以独立使用，不依赖于基类。
- 派生类拥有基类的全部成员函数和成员变量，无论private protected public
- 在派生类的各个函数成员中，不能访问基类中的private成员。
### 基本写法
```ruby
class 派生类名：public 基类名
{
    
}；
```
- 在派生类的成员函数跟基类的名字一样，参数一样，但行为不同，叫做覆盖。
### 派生类对象的内存空间
- 派生类对象的体积，等于基类对象的体积加上派生类对象自己的成员变量的体积。在派生类对象中，包含着基类对象，而且基类对象的存储位置位于派生类对象新增的成员变量之前。
```ruby 
class CBase{
    int v1,v2;
};
class CDerive:public CBase{
    int v3;
};
//此时的CDerive对象有三个变量：v1，v2,v3且v1,v2位于v3之前
```
# 继承关系和复合关系
- 类与类之间只有三种关系：没关系，继承关系，复合关系
- 继承：“是”的关系：基类A，派生类B，从逻辑上说，一个B对象也是一个A对象 
- 复合“有”关系：类C中有成员变量k,k是类D的对象，则C和D是复合关系，从逻辑上说，D对象时C对象的固有属性和组成部分
# 基类和派生类同名成员
```ruby
class base
{
    int j;
    public:
    int i;
    void func();
};

class derived:public base
{
    public:
    int i;//同名成员变量
    void access();
    void func();//同名成员函数
};
void derived::access()
{
    j=5;//error,j是基类私有成员变量，不能被派生类访问
    i=5;//引用的是派生类的i
    base::i=5;//引用的是基类的i
    func();//派生类
    base::func();//基类
}
derived obj;
obj.i=1;//派生类自己的i
obj.base::i=1;//派生类中基类的i
```
### 访问范围说明符
- 基类的private成员只能被基类的成员函数，基类的友元函数访问
- 基类的public成员可以被基类的成员函数、友元函数，派生类的成员函数、友元函数，以及其他函数访问
- 基类的protected成员可以被基类的成员函数、友元函数访问，可以被派生类的成员函数访问(访问当前对象的基类保护成员)
# 派生类的构造函数
- 派生类包含基类对象，执行派生类构造函数之前，先执行基类的构造函数
- 派生类交代基类初始化：
```ruby
构造函数名(形参表):基类名(基类构造函数实参表)
{
    
}
```

```ruby
class Bug
{
    private:
    int nLegs,nColor;
    public:
    int nType;
    Bug(int legs,int color);
    void PrintBug(){};
};
class FlyBug:public Bug
{
    int nWings;
    public:
    FlyBug(int legs,int color,int wings);
}
Bug::Bug(int legs,int color)
{
    nLegs=legs;
    nColor=color;
}
/*错误的FlyBug构造函数：
FlyBug::FlyBug(int legs,int color,int wings)
{
    nLegs=legs;//不能访问
    nColor=color;//不能访问
    nType=1;//ok
    nWings=wings;
}
*/

//正确的：
FlyBug::FlyBug(int legs,int color,int wings):Bug(legs,color)
{
   nWings=wings;
}

int main()
{
    FlyBug fb(2,3,4);
    fb.PrintBug();
    fb.nType=1;
    fb.nLegs=2;//error nlegs is private
    return 0;
}
```
- 创建派生类对象时：需要调用基类的构造函数：初始化派生类对象中从基类继承的成员
- 在执行一个派生类的构造函数之前，总是执行基类的构造函数
### 调用基类构造函数的两种方式：
- 显示方式：在派生类的构造函数中显示的表达基类的构造函数并提供参数
```ruby
derived::derived(arg_derived-list):base(arg_base-list)
//形参的参数写在基类的构造函数中
```
- 隐式方式：派生类的构造函数中省略基类构造函数的调用，派生类的构造函数自动调用默认的构造函数
- 派生类的析构函数在执行时，先调用派生类的析构函数，再调用基类的析构函数。
#### 包含成员对象的派生类的构造函数
```ruby
class Skill{
    public:
    Skill(int n){}
};
class FlyBug:public Bug
{
    int nWings;
    Skill sk1,sk2;
    public:
    FlyBug(int legs,int color,int wings);
};
FlyBug::FlyBug(int legs,int color,int wings):Bug(legs,color),sk1(5),sk2(color)
{
    nWings=wings;
}
```
- 在创建派生类的对象时，执行派生类的构造函数之前调用基类的构造函数去初始化派生类对象中从基类继承的成员再调用成员对象类的构造函数去初始化派生类对象成员中成员对象
- 执行完派生类的析构函数后调用成员对象类的析构函数再调用基类的析构函数
- 析构函数的调用顺序与构造函数相反
# public继承的赋值兼容规则
```ruby
class base{}；
class derived:public base{};
base b;
derived d;
```

- 派生类对象可以赋值给基类对象，基类对象不能赋值给派生类对象
```ruby
b=d;
```
- 派生类对象可以初始化基类引用
```ruby
base &br=d;
```
- 派生类对象的地址可以赋值给基类指针
```ruby
base *pb=&d;
```
# 直接基类和间接基类
- 类A派生类B，类B派生类C，类C派生类D...
- - 类A时类B的直接基类；类B是类C的直接基类，类A是类C的间接基类；类C是类D的直接基类，类A，B是类D的间接基类
- 在声明派生类的时候，只需要列出它的直接基类
