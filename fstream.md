## fstream

> 打开文件
```
#include <fsteam>
DataType :
ofstream //文件写操作
ifstream //文件读操作
fstream //文件读写操作

Fuction : 
void open(const char * filename,
	ios_base::openmode mode=ios_base::in | ios_base::out)

void open(const wchar_t *_Filename,
	ios_base::openmode mode= ios_base::in | ios_base::out,
	int prot = ios_base::_Openprot)；
	
/*filename   操作文件名
mode        打开文件的方式
prot         打开文件的属性                            //基本很少用到，在查看资料时，发现有两种方式*/

```
|mode|sense|
|------|------|
|ios::in|	为输入(读)而打开文件|
|ios::out|	为输出(写)而打开文件|
|ios::ate|	初始位置：文件尾|
|ios::app|	所有输出附加在文件末尾|
|ios::trunc|	如果文件已存在则先删除该文件|
|ios::binary|	二进制方式|

|prot|opertion|
|-|-|
|0	普通文件，打开操作
1	只读文件
2	隐含文件
4	系统文件|

```
可能会碰到ofstream out("Hello.txt"), ifstream in("..."),fstream foi("...")这样的的使用，并没有显式的去调用open（）函数就进行文件的操作，直接调用了其默认的打开方式，因为在stream类的构造函数中调用了open()函数,并拥有同样的构造函数，所以在这里可以直接使用流对象进行文件的操作，默认方式如下：
ofstream out("...", ios::out);
ifstream in("...", ios::in);
fstream foi("...", ios::in|ios::out);
```
> 关闭文件
```
function:
close()
将缓存中的数据释放并关闭文件

```

> 文本文件的读写

```
 // writing on a text file
    #include <fiostream.h>
    int main () {
	ofstream out("out.txt");
	if (out.is_open()) 
	{
	    out << "This is a line.\n";
	    out << "This is another line.\n";
	    out.close();
	}
	return 0;
    }
   //结果: 在out.txt中写入：
   This is a line.
   This is another line 
```
```
// reading a text file
    #include <iostream.h>
    #include <fstream.h>
    #include <stdlib.h>
    
    int main () {
	char buffer[256];
	ifstream in("test.txt");
	if (! in.is_open())
	{ cout << "Error opening file"; exit (1); }
	while (!in.eof() )
	{
	    in.getline (buffer,100);
	    cout << buffer << endl;
	}
	return 0;
    }
    //结果 在屏幕上输出
     This is a line.
     This is another line

```

> 流操作
```
流状态验证
bad()
如果在读写过程中出错，返回 true 。例如：当我们要对一个不是打开为写状态的文件进行写入时，或者我们要写入的设备没有剩余空间的时候。

fail()
除了与bad() 同样的情况下会返回 true 以外，加上格式错误时也返回true ，例如当想要读入一个整数，而获得了一个字母的时候。

eof()
如果读文件到达文件末尾，返回true。

good()
这是最通用的：如果调用以上任何一个函数返回true 的话，此函数返回 false 

```
```
获得和设置流指针(get and put stream pointers)
所有输入/输出流对象(i/o streams objects)都有至少一个流指针：

ifstream， 类似istream, 有一个被称为get pointer的指针，指向下一个将被读取的元素。
ofstream, 类似 ostream, 有一个指针 put pointer ，指向写入下一个元素的位置。
fstream, 类似 iostream, 同时继承了get 和 put
我们可以通过使用以下成员函数来读出或配置这些指向流中读写位置的流指针：

tellg() 和 tellp()
这两个成员函数不用传入参数，返回pos_type 类型的值(根据ANSI-C++ 标准) ，就是一个整数，代表当前get 流指针的位置 (用tellg) 或 put 流指针的位置(用tellp).

seekg() 和seekp()
这对函数分别用来改变流指针get 和put的位置。两个函数都被重载为两种不同的原型：

seekg ( pos_type position );
seekp ( pos_type position );
使用这个原型，流指针被改变为指向从文件开始计算的一个绝对位置。要求传入的参数类型与函数 tellg 和tellp 的返回值类型相同。

seekg ( off_type offset, seekdir direction );
seekp ( off_type offset, seekdir direction );
使用这个原型可以指定由参数direction决定的一个具体的指针开始计算的一个位移(offset)。它可以是：

ios::beg	从流开始位置计算的位移
ios::cur	从流指针当前位置开始计算的位移
ios::end	从流末尾处开始计算的位移

流指针 get 和 put 的值对文本文件(text file)和二进制文件(binary file)的计算方法都是不同的，因为文本模式的文件中某些特殊字符可能被修改。由于这个原因，建议对以文本文件模式打开的文件总是使用seekg 和 seekp的第一种原型，而且不要对tellg 或 tellp 的返回值进行修改。

```
> 获取二进制文件的大小

```
 // obtaining file size
    #include <iostream.h>
    #include <fstream.h>
    
    const char * filename = "test.txt";
    
    int main () {
	long l,m;
	ifstream in(filename, ios::in|ios::binary)readTrtFile;
	l = in.tellg();
	in.seekg (0, ios::end);
	m = in.tellg();
	in.close();
	cout << "size of " << filename;
	cout << " is " << (m-l) << " bytes.\n";
	return 0;
    }
   
   //结果:
   size of example.txt is 40 bytes.

```