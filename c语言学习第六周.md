- **字符类型**  
char是一种整数，也是一种特殊的类型：字符 character  
因为，可以用单引号表示字符的字面量， ''也是一个字符，printf和scanf中用%c来输入输出字符，'1'和1不相等，前者是字符，后者是整数，在计算机内部用49表示字符1，ASCII码
```
scanf("%d %c",&d,&c);
scanf("%d%c",&d,&c);
两者有区别，第一个读完整数还要把后面的空格读掉
第二个则是读完整数直接到后面
```
字符的运算
```
char c = 'A';
c++;
printf('%c\n',c);
结果是B
```
- **逃逸字符**  
用来表示无法印出的控制字符或特殊字符，由反斜杠\开头，后面跟上另一个字符
```
\b 回退一格  
\t 到下一个表格位
123 456
1   45    制表位
\n 换行 \r 回车
\'  \\
```
- **字符串**  
```
char word[] = {'h','e','l','l','o','!'};
字符数组，不是字符串，因为不能用字符串的方式做计算  
char word[] = {'h','e','l','l','o','!'，'\0'};
因为最后一个0，其便成为c语言的字符串
```
字符串表示以0结尾的一串字符，不可以用字符'0'  
0用来标志字符串的结束，但它不是字符串的一部分，计算字符串长度时不包括这个0  
字符串以数组的形式存在，以数组或指针的方式访问  
string.h中有很多处理字符串的函数  
字符串变量
```
char *str = "hello";
char word[] = "hello";
char line[10] = "hello"; 五个字符，再加上一个0，因此其实是6个字节
```
字符串常量  
"hello" 会被编译器变成一个字符数组放在某处，这个数组的长度是6，结尾还有表示结束的0  
两个相邻的字符串会自动连结，和java、python不同，不能用加号等运算符  
通过数组的方式可以遍历字符串，唯一特殊的是字符串字面量可以用来初始化字符数组
- **char\*  和 char s []**
```
char *s = "hello world";
char *s2 = "hello world";
```
s和s2都指向某个地址的字符数组，而这儿的字符串是只读的，因此不能用s[0]="b"修改  
s是一个指针，初始化指向一个字符串常量，由于这个常量所在的位置，所以s实际上是const char *s，但由于历史的原因，编译器允许不带const的写法，但是试图对s所指向的字符串做修改会导致严重的错误  
如果需要修改，应该用数组的方式来定义字符串  
```
char s[] = "hello world";
```
因为通过这种方式定义的字符数组就在本地，而不在指针指向的某个位置
```
char *s = "hello world";
char s[] = "hello world";
```
作为数组，这个字符串在这里，作为本地变量空间自动被回收；  
而作为指针，不知道这个字符串在哪里，处理参数，动态分配空间  
如果要构造一个字符串，用数组，如果要处理一个字符串，用指针  
因此，char* 并不一定表示字符串，它表示指向一个字节，或者连续的字节，但不一定是字符串，就像int*一样，可能指向一个整数，也可能指向一个数组  
只用当char* 所指的字符数组有结尾的0，这时候才能说它所指向的是字符串
- **字符串输入输出**  
```
char string[8];
scanf("%s",string);
printf("%s",string);
```
%s读入一个单词，到空格，tab，回车为止
但是这个scanf是不安全的，因为我们不知道要读入的内容的长度  
可以在%和s之间加上7，即表明最多只读前七个
```
char* string;
scanf("%s",string);
常见的错误
```
以为char*是字符串类型，定义来一个字符串变量就可以直接使用，由于没有对string初始化为0.所以不一定每次运行都出错
```
char buffer[100]="";
这是一个空字符串，则buffer[0] =="\0"
```
- **字符串函数**  
string.h
```
#include<string.h>
```
```
strlen
size_t strlen(const char* s);
返回s的字符串长度，不包括结尾的0

strcmp
int strcmp(const char* s1,const char* s2);
比较两个字符串，返回
0：s1 == s2
1: s1>s2
-1: s1<s2

char s1[] = "abc";
char s2[] = "abc";
printf("%d\n",s1 == s2);
printf("%d\n",strcmp(s1,s2));
两个数组一定不会是相同的地址，因此s1 == s2，永远为false
不想等时会给出s1和s2不想等字符的差值

strcpy
char* strcpy(char* restrict dst,const char *restrict src);
将src的字符串拷贝到dst
restrict表明src和dst不重叠
返回dst
为了能够链起代码来

strcat
char *strcat(char *restrict s1,const char *restrict s2);
将s2拷贝到s1后面接成一个长的字符串
返回s1，s1必须具有足够的空间

strcpy和strcat都可能存在安全问题
即如果目的地没有足够的空间

安全版本
char *strncpy(char *restrict dst,const char *restrict src,size_t n);
char *strncat(char *restrict s1,const char *restrict src,size_t n);
int strncmp(const char *s1,const char *s2,size_t n)

在字符串中找字符
char *strchr(const char *s,int c);
char *strrchr(const char *s,int c);
第一个表示从左边找过来c第一次出现的地址，
返回指针，指向所要找的字符
第二个表示葱花右边找过来
返回NULL表示没有找到

```
