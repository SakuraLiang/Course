# 友元函数
- 一个类的友元函数可以访问该类的私有成员
- 可以将一个类的成员函数(包括构造，析构函数)定义为另一个类的友元。
```ruby
class B{
    public:
    void function();
};

class A{
    friend void B::function();
};
```
# 友元类
- A是B的友元类：A的成员函数可以访问B的私有成员
```ruby
class CCar{
    private:
    int price;
    friend class CDriver;//声明CDriver为友元类
};
class CDriver{
    public:
    CCar mycar;
    void ModifyCar(){
        mycar.price+=1000;//CDriver是CCar的友元类，可以访问其私有成员
    }
};
int main ()
{
    return 0;
}
```
- 友元类之间的关系不能传递，不能继承。
