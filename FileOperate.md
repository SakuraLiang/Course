# 文件操作
#### 顺序文件：
有限字符构成的顺序字符流
#### 文件流类
：ifstream, ofstream, fstream
#### 派生关系
:istream, ostream:ios; istream:istream  iostream:istream ostream;   ofstream:ostram;  fsteam:iostream;
#### 读写操作
利用读写指针进行相应位置的操作
#### 建立文件
-  
```ruby
ofstream outFile("文件名",ios::out|ios::binary);
```
ios::out(输出到文件,删除原有内容)/ios::app(输出到文件，保留原有内容)
ios::binary(打开文件形式,二进制)
- open函数 
```ruby
ofstream fout;
fout.open("文件名",ios::out|ios::binary);

```
