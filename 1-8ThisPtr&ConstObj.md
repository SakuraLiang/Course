# This指针
- 作用：指向成员函数所作用的对象。非静态成员函数中可以直接使用this来代表指向该函数作用的对象。
```ruby
class A{
    int i;
    public:
    void Hello(){cout<<"Hello"<<endl;}
};
int main()
{
    A*p=NULL;
    p->Hello();
}
//输出Hello
```

- 静态成员函数中不能使用This指针，因为静态成员函数并不具体作用于某个对象，因此，静态成员函数的真实的参数的个数，就是程序中写出的参数个数

# 常量对象，常量成员函数和常引用
- 常量对象：如果不希望某个对象的值被改变，则定义该对象的时候可以在前面加const关键字
```ruby
class Demo{
    private:
    int value;
    public:
    void SEtValue(){}
};
const Demo Obj;//一旦初始化完成，其值就不能再被修改
```
- 常量成员函数：在类的成员函数说明后面可以加const关键字，则该成员函数成为常量成员函数。常量成员函数执行期间不应修改其作用的对象。在常量成员函数中不能修改成员变量的值(静态成员变量除外)，也不能调用同类的非常量成员函数 (静态成员函数除外)。
```ruby
class Sample
{
    public:
    int value;
    void GetValue() const;
    void Func(){};
    Sample(){}
};
void Sample::GetValue() const
{
    value=0;//wrong
    func();//wrong
}
//这个常量成员函数企图修改成员变量的值，企图调用成员函数。
```
- main函数中的常量对象：
```ruby
int main(){
    const Sample o;
    o.value=100;//error,常量对象不可被修改
    o.func();//error,常量对象上不能执行非常量成员函数
    o.GetValue();//ok,常量对象上可以执行常量成员函数
}
```
### 常量成员函数的重载
- 两个成员函数，名字和参数表都一样，但是一个是const，一个不是，也算重载。而非重复定义。
```ruby
#include<iostream>
using namespace std;

class CTest
{
    private:
    int n;
    public:
    CTest(){n=1;}
    int GetValue() const {return n;}//常量成员函数
    int GetValue() {return 2*n;}//非常量成员函数
};
int main()
{
    const CTest objTest1;//常量对象
    CTest objTest2;//非常量对象
    cout<<objTest1.GetValue()<<" "<<objTest2.GetValue()<<endl;
    return 0;
}//即常量对象调用常量成员函数，非常量对象调用非常量成员函数
//结果
1 2
```
- 常引用：引用前面可以加const关键字，成为常引用。不能通过常引用，修改其引用的值,但变量自身是可以修改的
```ruby
const int &r=n;
r=5;//error
n=4;//ok
```
- 作用：对象作为参数时，生成该参数需要调用复制构造函数，效率比较低。用指针作参数，代码又难看...so...
- 
```ruby
class Sample{
    ...
};
void PrintfObj(Sample & o)
{
    ...
}//引用作为函数参数，当形参o改变时，实参也有可能被改变
 
 此时把
