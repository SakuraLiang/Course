# 流插入运算符的重载
- cout是在iostream中定义的，ostream类的对象
- <<能用在cout上是因为，在iostream里对<<进行了重载
```ruby
ostream & ostream::operator<<(int n)
{
  ....
  reutrn *this;
}//返回值类型仍为ostream才能进行连续的重载函数调用
```

```ruby
class CStudent{
    public: int nAge;
};
ostream & operator<<(ostream &o,const CStudent &a)
{
    o<<s.nAge;
    return o;
}
int main()
{
    CStudent s;
    s.nAge=5;
    cout<<s<<"hello";
    return 0;
}
```
# 自加自减运算符的重载
- 有前置和后置之分
- 前置运算符作为一元运算符重载
1. 重载为成员函数时：
```ruby
T operator++();
T operator--();
//是无参的
```
2. 重载为全局函数：
```ruby
T operator ++(T);
T operator --(T);
//是有参数的
```
- 后置运算符作为二元运算符重载
- - 区别于前置运算符，多写一个参数，无具体意义
1. 重载为成员函数
```ruby
T operator ++(int);
T operator --(int);
```
2. 重载为全局函数
```ruby
T operator++(T,int);
T operator--(T,int);
```


```ruby
#include<iostream>
using namespace std;
class CDemo{
    private:
    int n;
    public:
    CDemo(int i=0):n(i){}
    CDemo operator++();//前置
    CDemo operator--(int);//后置
    operator int (){return n;}
    friend CDemo operator--(CDemo &);
    friend CDemo operator--(CDemo &,int);
};
CDemo CDemo::operator++()
{
    n++;
    return *this;
}
CDemo CDemo::operator++(int k){
    CDemo tmp(*this);
    n++;
    return tmp;
}
CDemo operator--(CDemo & d){//前置
    d.n--;
    return d;
}
CDemo operator--(CDemo & d,int){//后置
    CDemo tmp(d);
    d.n--;
    return tmp;
}
int main()
{
	CDemo d(5);
	cout<<(d++)<<",";
	cout<<d<<",";
	cout<<(++d)<<",";
	cout<<d<<endl;
	cout<<(d--)<<",";
	cout<<d<<",";
	cout<<(--d)<<",";
	cout<<d<<endl;
	return 0; 
}//烂代码，不知道怎么运行而且不知道怎么改
```
### 运算符重载注意事项
- C++不允许定义新的运算符
- 重载后的运算符的含义应该符合日常习惯
- 运算符重载不能改变运算符的优先级
- 以下运算符不能被重载:"." "," "::" "?:" sizeof
- 重载运算符(),[],->或者赋值运算符=时，重载函数必须声明为类的成员函数
