# const关键字的用法
#### 定义常量

```ruby
const int MAX_VAL=23;
const doule Pi=3.14;
const cahr*SCHOOL_NAME="Peking University";
```
#### 定义常量指针
- 不可通过常量指针修改指向的内容，指向可以变化
```ruby
int n,m;
const int *p=&n;
*p=5;//编译出错
n=4;//正确
p=&m;//正确
```
- 不能把常量指针赋给非常量指针，反过来可以。
```ruby
const int *p1;
int *p2;
p1=p2;//okay
p2=p1;//error
p2=(int *) p1;//okay,强制类型转换
```
- 函数参数为常量指针，可以避免函数内部不小心改变参数指针所指地方的内容。
```ruby
void MyPrintf(const char *p)
{
    strcpy(p,"this");//error,strcpy的第一个参数应当是char型指针，而p是const char型指针，const char型不能赋给char型
    printf("%s",p);//okay
}
```
- 定义常引用
