# 构造函数
 ### 基本概念
成员函数的一种，名字与类名相同，可以有参数，不能有返回值(void)作用是对对象进行初始化，给成员变量赋初值等。如果定义类时没有写构造函数，则编译器生成一个默认的没有参数的构造函数，不做任何操作。只要有对象生成就一定会调用构造函数。构造函数可以有多个，参数表不同。
### 构造函数作用
1. 执行必要的初始化工作。有了构造函数不用再写初始化函数。
2. 有时对象没有初始化就使用，会导致程序出错

```ruby
class Complex{
    private:
      double real,image;
    public:
      void Set(double r,double i);
};//编译器会自动生成默认构造函数
Complex c1;//默认构造函数调用
Complex *pc=new Copmlex;//默认构造函数被调用
```
- 编译器默认的无参构造函数其缺省值是随机的
```ruby
#include<iostream>
using namespace std;
class Complex{
	private:
		int real,image;
	public:	    
		void Set(int r1,int i1)
		{
			real=r1;
			image=i1+1;
		}
		int OutReal()
		{
			return real;
		}
		int OutImage(){
			return image;
		}
}; 
int main()
{
	Complex A;
	//A.Set(3,4);省去这一步时，输出的值是36 0,运行这一步时，输出的值是3,5
	cout<<A.OutReal()<<" "<<A.OutImage()<<endl;
	return 0;
}
```
- 如果自己写的构造函数都是有参数的，在生成对象时没有用相应的参数初始化，则会报错。
```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
		int real,image;
	public:	    
         Complex(int r1/**=0**/,int i1/**=0**/)缺掉这一步时，如果生成对象时没有初始化，则报错，如果生成对象时有初始化，则不会报错。
		{
			real=r1;
			image=i1+1;
		}
}; 
int main()
{
	Complex A/**(3,4)**/;//在构造函数不缺的情况下，缺掉这一步时输出0,1，运行这一步时输出3,5
	cout<<A.real<<" "<<A.image<<endl;
	return 0;
}
```
- 即有缺省值才可以缺省
-构造函数也可重载，名字都为类名，只是参数列表不同。
 3. 构造函数在对象数组中的作用
- 数组中的不同元素的即每一个对象都会调用相应的构造函数。
- 如果是类的指针数组，由于元素是用指针指向的地址，当没有调用构造函数时，指针就没有明确指向哪里
```ruby
class Test
{
    public:
    Test(int n){}//1
    Test(int n,int m){}//2
    Test(){}//3
};
Test array1[3]={1,Test(1,2)};//三个元素分别用1,2,3初始化
Test array2[3]={Test(2,3),Test(1,2),1};//三个元素分别用2,2,1初始化
Test *parray[3]={new Test(4),new Test(1,2)};//只有两个元素分别调用了1,2，第三个元素没有调用
```
# 复制构造函数
- 基本概念：只有一个参数，即对同类对象的引用。形如X：:X(X&)或X::X(const X&)。
 同样，一个类总是有复制构造函数的，如果写的时候没有，编译器会默认生成一个复制构造函数。
```ruby
/**没有自己写的构造函数和复制构造函数，编译器默认生成**/
class Complex{
    private:
    double real,image;
};
Complex c1;//调用缺省无参构造函数
Complex c2(c1);//调用缺省无参复制构造函数
```
- 复制构造函数所做的事就是把c1的值全部赋给c1
- 复制构造函数的参数一定只能是同类的引用，不能是同类的对象
#### 复制构造函数起作用的三种情况
1.用一个对象去初始化另一个对象
```ruby
Complex c2(c1);
Complex c2=c1;
//两语句等价，都是初始化语句而非赋值语句
```
2.某函数的形参是类A的对象，那么该函数被调用时，类A的复制构造函数将被调用。
```ruby 
class A{
    public:
    A(){}//构造函数
    A(A&a){}//复制构造函数
};
void Func(A a1){}//参数是类A的对象
int main()
{
    A a2;
    Func(a2);//调用复制构造函数
    return 0;
}
```

```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
		int real,image;
	public:	    
         Complex(){}
         Complex(Complex &c)
		 {
         	real=c.real +1;
         	image=c.image+1;
         	cout<<real<<" "<<image<<"copy constructor"<<endl;
		 }
	
};
void Func(Complex c1){}
int main()
{
	Complex A;
	Func(A);
	return 0;
}
//输出 37 1constructor。因为构造函数都是无参的，所以缺省值为随机值。
```
- 系统的复制构造函数是会执行复制操作的，自己写的就不一定了
```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
		int real,image;
	public:	    
         Complex()
		 {
		 real=3;
		 image=4;
		 }
		 /**Complex(Complex &c){
		 }**/
};
void Func(Complex c1){cout<<c1.real<<" "<<c1.image<<endl;}
int main()
{
	Complex A;
	Func(A);
	return 0;
}
如果执行那步操作，输出的为1512304 0，如果不执行，输出3 4.
```
3.函数返回值是类A的对象，函数返回时，类A的复制构造函数被调用。此时调用的函数是用来初始化作为返回值的类A的对象。
```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
		int real,image;
	public:	    
         Complex(int r=0,int i=0)
		 {
		 real=r;
		 image=i;
		 }
		 Complex(Complex &c)
		 {
		 	real=c.real+3;
		 	image=c.image+3;
		 	cout<<"copy constructor"<<endl;
		 }	 
};
Complex Fun(Complex c2)
	{
		return c2;
	}//c2就是初始化返回的Fun的参数，两者值不一定相等，取决于复制构造函数的写法	
int main()
{
	Complex a(2,3);
	Fun(a);//此时的Fun(a)只是一个临时对象
	return 0;
}
//输出结果为两行copy constructor，一次是由于Complex类的对象作为了函数的参数，当函数被调用时，复制构造函数调用，还有一次是Complex的对象作为函数返回值
```

```ruby
#include<iostream>
using namespace std;
class Complex{
	public:
		int real,image;
	public:	    
         Complex(int r=0,int i=0)
		 {
		 real=r;
		 image=i;
		 }
		 Complex(Complex &c)
		 {
		 	real=c.real+3;
		 	image=c.image+3;
		 	cout<<"copy constructor"<<endl;
		 }	 
};
Complex Fun(Complex c2)
	{
		return c2;
	}	
int main()
{
	Complex a(2,3);
	Fun(a);
	cout<<endl;
	cout<<Fun(a).real<<" "<<Fun(a).real<<" "<<Fun(a).image<<endl; 
	return 0;
}//输出结果为

copy constructor
copy constructor

copy constructor
copy constructor
copy constructor
copy constructor
copy constructor
copy constructor
8 8 9
```
