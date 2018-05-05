# 类型转换构造函数
- 目的：实现类型的自动转换
- 特点：
1. 只有一个参数
2. 不是复制构造函数
- 编译系统会自动调用转换构造函数，同时建立一个临时对象或者变量
```ruby
 #include<iostream>
using namespace std;
class Complex{
	public:
		double real,image;
	public:	    
         Complex(double r,double i)
		 {
		 real=r;
		 image=i;
		 }
		 Complex (int i)
		 {
		 	real=i;
		 	image=0;
		 	cout<<"Type conversion"<<endl;
		 }	
		  
};	
int main()
{
	Complex a(2,3);
	cout<<endl;
	cout<<a.real<<" "<<a.image<<endl; 
	a=9;//9被转换为一个临时对象
	cout<<a.real<<" "<<a.image<<endl; 
	return 0;
}

结果为

2 3
Type conversion
9 0
```
