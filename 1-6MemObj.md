# 成员对象和封闭类
- 成员对象：一个类的成员变量是另一个类的对象
- 包含成员对象的类叫封闭类
- 定义封闭类的构造函数时，添加初始化列表：
```ruby
类名：：构造函数(参数表)：成员变量1(参数表),成员变量2(参数表),...
{
    
}
```
- 成员对象初始化列表中的参数可以是任意复杂度的表达式，函数、变量表达式中的函数。变量有定义。
### 调用顺序：
- 封闭类对象生成时，先执行所有成员对象的构造函数，再执行封闭类的构造函数。
- 成员对象的构造函数调用顺序与成员对象在类中的说明顺序一致，与成员初始化列表中出现的顺序无关。
- 封闭类对象消亡时，先执行封闭类的析构函数，在执行成员对象的析构函数。
- 析构函数和构造函数的调用顺序刚好相反。
