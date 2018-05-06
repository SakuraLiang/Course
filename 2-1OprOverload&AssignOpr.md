# 运算符重载
- 运算符重载：对已有的运算符赋予多重的含义，使同一运算符作用于不同类型的数据是，有不同类型的行为。
- 运算符重载的实质是函数重载
```ruby
返回值类型 operator 运算符(形参表)
{
    ...
}
```
- 在程序编译时，会把含运算符的表达式 转换为 对运算符函数的调用。把运算符的操作数 转换为 运算符函数的参数。
- 运算符多次被重载，就可以根据实参类型决定对运算符函数的调用。
### 运算符重载为普通函数
```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
	int real,image;
	Complex(int r=0,int i=0){
		real=r;
		image=i;
	}
}; 
Complex operator+(const Complex &a,const Complex &b)
{ 
   Complex temp;
   temp.real=a.real+b.real;
   temp.image =a.image+b.image;
   return  temp;
} 
int main()
{
	Complex A(1,3);
	Complex B(5,6);
	cout<<(A+B).real<<" "<<(A+B).image<<endl;
	return 0;
}
//输出结果为6 9
```
- 重载为普通函数时，参数个数为运算符目数。
### 运算符重载为成员函数
```
#include<iostream>
using namespace std;
class Complex{
	public:
	int real,image;
	Complex(int r=0,int i=0){
		real=r;
		image=i;
	}
	Complex operator+(const Complex &b)
	{ 
     real+=b.real;
     image+=b.image;
     cout<<real<<" "<<image<<endl;
   return  *this;
   }	
}; 
int main()
{
	Complex A(1,3);
	Complex B(5,6);
	Complex C;
	C=A+B;
	cout<<"C:"<<C.real<<" "<<C.image<<endl;
	cout<<"(A+B).real:"<<(A+B).real<<endl;
	cout<<"(A+B).image:"<<(A+B).image<<endl;
	return 0;
}
输出结果：
6 9
C:6 9
11 15
(A+B).real:11
16 21
(A+B).image:21
- 每一次调用运算符函数，都会把其所属的对象的变量的值改变(因为这种情况下不是const引用)
```
- 还有个有趣的现象：
```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
	int real,image;
	Complex(int r=0,int i=0){
		real=r;
		image=i;
	}
	Complex operator+(const Complex &b)
	{ 
     real+=b.real;
     image+=b.image;
     cout<<real<<" "<<image<<endl;
   return  *this;
   }	
}; 
int main()
{
	Complex A(1,3);
	Complex B(5,6);
	Complex C;
	C=A+B;
	cout<<"C:"<<C.real<<" "<<C.image<<endl;
	cout<<"(A+B).real:"<<(A+B).real<<endl<<"(A+B).image:"<<(A+B).image<<endl;
	return 0;
}
//输出的结果为：
6 9
C:6 9
11 15
16 21
(A+B).real:16
(A+B).image:15
//大概是因为...因为啥...
```
# 赋值运算符“=”重载
- 在对象与对象之间，“=”运算符就能直接使用，可以将后者的全部内容一一对应赋给前者
### 赋值运算符两边的类型不匹配
- 需要将“=”重载，且只能重载为成员函数。
#### 编写一个长度可变的字符串类String：
- 包含一个char*类型的成员变量指向动态分配的存储空间。该空间用于存放“\0”结尾的字符串
```ruby
class String {
private:
  char * str;
public:
  String(): str(NULL) { }  //构造函数
  const char * c_str() { return str; }  // char * p=s.c_str();
  char * operator=(const char * s);
  ~String();
};

char * String::operator=(const char * s)
{
  if(str)
    delete [] str;
  if(s) {
    str = new char[strlen(s)+1];
    strcpy(str,s);
  }
  else
    str=NULL;

  return str;
}

String::~String()
{
  if(str)
    delete [] str;
}

int main()
{
  String s;
  s="Good Luck!";
  cout<<s.c_str()<<endl;
  //  String s2="Hello!";  //初始化语句调用构造函数 String(const char *)
  s="Hello World!";
  cout<<s.c_str()<<endl;

  return 0;
}
```
### 赋值运算符重载的意义
- 浅复制/浅拷贝：执行逐个 字节 的复制工作。如果某个类的成员有指针，这一类的两个对象直接浅复制只会将后者指针指向的地址赋给前者对应的指针。这样就会有两个指针指向同一片存储空间，且前者指针原来指向的存储空间将没有指针控制的情况，会导致前者指针原来指向的存储空间变为内存垃圾，且在两个指针消亡时，同一片内存空间会被delete两次。(个人认为，这个问题倒是蛮好解决的...)
- 深复制/深拷贝：将一个对象中指针变量指向的内容赋值到另一个对象中指针成员指向的地方。
- 完成深复制：在class MyString添加新的成员函数
```ruby
String & operator=(const String & s){
    if(str==s.str) return *this//这样才能使s=s语句成立
    if(str) delete []str;
    str=new char[strlen(s.str)+1];
    strcpy(str,s.str);
    return *this;
}
```
# 运算符重载为友元函数
- 重载为友元函数的情况：成员函数不能满足使用要求，普通函数不能访问私有成员。
