## 变量
```
#include<stdio.h>
int main()
{
    int price=0;
    printf("请输入金额（元）：");
    scanf("%d",&price);
    int change = 100-price;
    printf("找零为%d元。\n",change);
    return 0;
}
```
- price =0;定义了一个变量，类型是int，初始值是0  
变量是保存数据的地方<类型名称> <变量>;  
变量的名字是一个标识符，字母数字下划线，数字不可以出现在第一个位置上，不能有c语言的保留字
- 程序设计中=赋值是一个动作  
当赋值发生在定义变量时，就是变量的初始化，虽然没有强制要求初始化，但第一次被使用前应该被赋值一次。如果没有赋值，那么其在内存的什么地方，那个地方原本有什么值，其就是什么。  
- c语言是一种有类型的语言，变量使用前必须定义或声明，过程中不能改变类型  
- ANSIC 只有在开头定义变量，C99可以在其他地方定义
- scanf和printf后面的f是formated，格式化，&到指针再讲  
- 如果输入是“hello”，结果会是100，因为输入的不是字，因此默认为0
```
int a= 0;
int b=0
scanf("%d %d",&a,&b);
printf("%d %d",a,b);
return 0;
```
- 如果在scanf引号里将空格变为“,”逗号，输入“1 2”输出的结果就会错误，应该输入“1，2”，scanf里面都是要输入的  
## 常量  
 直接写在程序你的是直接量（literal），如100  
但更好的办法是定义一个常量，给其一个名字  
```
const int AMOUNT =100;
这也是c99的写法
```
- const是一个修饰符，放在变量前面表示这个变量不能被修改read-only variable is not assignable
## 数据类型
两个整数运算的结果只能是整数，在python3中不会如此  
浮点数，带小数点的数值，浮点的本意是表示小数点是浮动的，是计算机内部表达非整数的一种方式，与其相对的是定点数，但c中不会出现  
12改成12.0，%d改成%f ，或者int改成double，%d改成%lf
```
#include <stdio.h>

int main()
{
	printf("Please insert foot and inch:");
	double foot;
	double inch;
	scanf("%lf,%lf",&foot,&inch);
	printf("%f\n",(foot+inch/12)*0.3048);
	
	return 0;
}
```
double是双精度浮点数，单精度浮点数是float  
10/3.0*3的结果是10.0
## 表达式
运算符和算子
```

#include <stdio.h>
int main(){
    int hour1,minute1;
    int hour2,minute2;
    scanf("%d %d",&hour1,&minute1);
    scanf("%d %d",&hour2,&minute2);
    int t1 = hour1*60 + minute1;
    int t2 = hour2*60 + minute2;
    int t = t2 - t1;
    printf("时间差是%d时%d秒",t/60,t%60);
    return 0;
}
```
- **运算符优先级**  
a*-b 先做-b，单目加减优先级最高  
在c中，赋值是一个运算符，赋值运算也是有结果，a=b=6，赋值自右向左结合，先做b=6，再将b=6赋给a  
int c=1+(b=a) 这种是嵌入式赋值，但不利于阅读  
- **交换两个变量**  
找个中间容器，写程序要熟悉套路  
- **符合赋值**  
total+=5  
```
++和-- 是递增和递减运算符，单目运算符，算子必须是变量  
a++和++a都表示a=a+1，但我们知道运算符都有结果，a++的结果是a加1以前的值，而++a则是加1之后的值
```     