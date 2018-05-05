# 析构函数
### 基本概念：
- 成员函数的一种
- 名字与类名相同
- 在前面加~
- 没有参数和返回值
- 一个类最多只有一个析构函数
- 对象消亡前的处理，比如释放相应的内存空间，会被自动调用
- 定义类时如果没有自己写，编译器会自动生成缺省析构函数，但不涉及用户申请的内存释放等清理工作，一旦定义了析构函数，编译器就不会生成析构函数。
```ruby
class String{
    private:
    char*p;
    public:
    String (){
        p=new char[10];
    }
    ~String()
};
String::~String(){
    delete []p;
}
```
## 析构函数与数组
- 对象数组生命周期结束时，每个元素的析构函数都会被调用
```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
		double real,image;
	public:	    
         Complex(double r=0,double i=0)
		 {
		 real=r;
		 image=i;
		 }
		 ~Complex()
		 {
		 	cout<<"Destructor"<<endl;
	     }
};	
int main()
{
	Complex array[2];
    cout<<"End Main"<<endl;
	return 0;
}

输出结果
End Main
Destructor
Destructor
```

### 析构函数和delete运算符
- delete运算导致析构函数调用，每个对象delete一次，析构函数调用一次
