- **取地址运算**  
sizeof 在内存中占据的字节  
int 4个字节 double 8个字节  
scanf("%d",&x);中的&运算符，获得变量的地址，它的操作数必须是变量  
```
int main(){
    int i = 0;
    printf("0x%x\n",&i);
    //printf("%p\n",&i);
    return 0;
}

//得到一个warning，并给出一个16进制的值  

因为输出一个地址，希望你用%p

int main(){
    int i = 0;
    int p;
    p = int(&i);
    printf("0x%x\n",p);
    printf("%p\n",&i);
    printf("%lu",sizeof(int));
    printf("%lu",sizeof(&i));
    return 0;
}
用32位时两者相等，64位架构时则非
在64位下，sizeof，前者为4，后者地址为8个字节
但在32位架构下都是4个字节

```
&只能对变量取地址
i和p的地址相邻，相差4个字节，i比较大，因其分配在内存堆栈的地方，分配是自顶向下来分配的
```
//数组
int main(){
    int a[10];
    printf("%p",&a);
    printf("%p",a);
    printf("%p",&a[0]);
    printf("%p",&a[1]);  
    return 0;
}
前三者地址相差s
0xbff8dd44
0xbff8dd44
0xbff8dd44
0xbff8dd48
```
- **scanf**  
scanf中有一个办法可以接受到地址，指针，就是保留地址的变量
```
int* p=&i;
//*表示p是一个指针，其指向的是一个int，
//将i的地址交给了p，p指向了i
int* p,q;
int *p,q;
//这两个都表示p是一个指针，而q是普通变量，
//因此我们并不是把*加给了int，而是加给了p
//即*p是一个int，于是p是一个指针，
//而不是p是一个int*类型
```
指针变量的值是内存的地址，普通变量的值是实际的值，指针变量的值是具有实际值的变量的地址
- **作为参数的指针**  
```
void f(int *p)
在被调用时得到某个变量的地址
int i=0;f(&i);
在函数里面可以通过这个指针访问外面的i
```
- **访问那个地址上的变量**  
*是一个单目运算符，用来访问指针的值所表示的地址上的变量  
可以做右值也可以做左值  
```
int k = *p;
*p = k+1;

int i;scanf("%d",i);
编译不报错，是因为编译器以为你传入的是一个地址，但你传入却是一个整数i，
因此他没有将传入的数值写入到i这个变量的地址内，而是写入了名为i（比如6）的地址的位置，地址6很小，有重要的内容
```
```
void f(int *p);
void g(int k);

int  main(){
    int i = 6;
    printf("&i=%p\n",&i);
    f(&i);
    g(i);
    return 0;
}

void f(int *p){
    printf("p =%p\n",p);
    *p =26;
}

void g(int k){
    printf("k =%d\n",k);
}

```
- **指针与数组**  
函数参数里的数组的sizeof返回的是int*的长度，而不是int[]
函数中的a[]和main中a[]是同一个  
函数里的a[]是一个指针，所以，int a[]可以改成int *a  
函数参数表中的数组是一个指针，
```
sizeof(a)= sizepof(int*)
```
因此，以下四种原型声明是等价的
```
int sum((int *ar,int n);
int sum(int*,int);
int sum(int ar[],int);
int sum(int [],int);
```
数组变量是特殊的指针  
数组变量本身就表达地址，
```
int a[10];int*p= a; //无需用&取地址  
```
但是数组的单元表示的是变量，需要用&取地址
a == &a[0]  
[]运算符可以对数组做，也可以对指针做
```
p[0]<==>a[0] <==>*p
即使*P是单个变量，p[0]也可以将单个变量视为一个长度为1的数组，而p[0]即是得到第一个地址上的变量
```
*运算符可以对指针做，也可以对数组做
```
int a[10] ={10,};
这个时候*a的值是10，即数组第一个元素
```
数组是const的指针，所以不能相互之间赋值
```
int a[10];
int b[10];
b = a;
这是错误的
int *q = a;
则是可以的
因为
int b[];可以看做是 int *const b； 常量是不能改变的
```


