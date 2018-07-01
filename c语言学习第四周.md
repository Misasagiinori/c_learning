- **数组**  
```
int number[100];
number[cnt] = x;
```
<类型>变量名[元素数量]  
元素数量必须是整数，c99之前元素数量必须是编译时确定的字面量  
数组是一种容器，其中所有元素具有相同的数据类型，一旦创建不能改变大小，数组中的元素在内存中时连续依次排列的  
编译器运行环境不会检测数组下标是否越界，一旦运行，可能造成崩溃，segmentation fault
```
#include<stdio.h>

int main(){
	double sum = 0.0;
	int cnt,x;
	printf("请输入数组长度:");
	scanf("%d",&cnt);
	int i = cnt;
	int numbers[cnt];
	while(cnt>0){
		scanf("%d",&x);
		numbers[cnt-1] = x;
		sum+=x;
		cnt--;
		}
	double average = sum/i;
	printf("平均数是%f\n",average);
	for(cnt=i;cnt>0;cnt--){
		if(numbers[cnt-1]>average){
			printf("%d ",numbers[cnt-1]);
		}
    }
	return 0;
}
```
字符也可以做下标，因为字符用的ASCII码在计算机中是以整数存储的，但字符做下标有一定的范围（32，176）
```
int a[255];
a['A'] = 1;
```
- **函数**  
```
//用函数找出素数

#include <stdio.h>
int isPrime(int x){  //素数判断
	int i; 
	int ret = 1;
        for(i=2;i<x;i++){
            if(x%i==0){
                ret = 0;
                break;
            }
        }
    return ret;
}
int main(){
    int x;
    int cnts,cntd;
    printf("请输入要查找素数的范围（空格分隔）：");
    scanf("%d %d",&cnts,&cntd);
    for(x=cnts;x<cntd;x++){
        if (isPrime(x)){  //使用上述函数
            printf("%d ",x);
        }
    }
    return 0;
}
```
代码复制意味着代码质量不良  
函数是一块代码，接收零个或多个参数，做一件事情，并返回零个或一个值
```
#include<stdio.h>
void sum(int begin,int end){ //函数头
    int i;                   //函数体
    int sum = 0;
    for(i=begin;i<=end;i++){
        sum+=i;
    }
    printf("%d到%d的和是%d",begin,end,sum);
}

int main(){
	sum(2,7);
	return 0;
}

```
sum是函数名；void是函数的返回类型，void的意思是不返回任何结果；圆括号表明sum是一个函数；圆括号里面是参数表，用逗号分割；调用时，函数名（参数值）；就是没有参数，也要加上圆括号
- **从函数返回值**  
return停止函数的执行，并返回一个值；return；return 表达式;  
return最好保持单一出口  
没有返回值的函数：void；不能使用带值的return，可以没有return；调用时不能做返回值的赋值
- **函数的原型声明**  
```
#include<stdio.h>
void sum(int ,int );

int main(){
	sum(2,7);
	
	return 0;
}

void sum(int begin,int end){ //函数头
    int i;                   //函数体
    int sum = 0;
    for(i=begin;i<=end;i++){
        sum+=i;
    }
    printf("%d到%d的和是%d",begin,end,sum);
}
```
将函数的头放在main()函数前面，叫做函数的原型声明，后面真正的位置叫做函数的定义,还会检查声明和定义是否是否是一致的，函数的原型声明里面可以不写参数的名字，但通常会留着，以便于阅读。
- **参数传递**  
```
#include <stdio.h>
void cheer (int i){
    printf("cheer,%d\n",i);
}
int main(){
    cheer(2.4);
    
    return 0;
}

结果会输出2，严格的编译器会给个warning
```
调用函数时给的值与参数的值类型可以不匹配，这是c语言传统上最大的漏洞  
编译器总是替你将类型转换好，但这很可能不是你所期望的，后续的c++和java对这方面很严格。  
- **调用函数时传过去的到底是什么？**
```
#include <stdio.h>
void swap (int a,int b){
    int t;
    t = a;
    a = b;
    b = t;
}

int main(){
    int a = 5;
    int b = 6;
    swap(a,b);
    printf("%d %d\n",a,b);
    return 0;
}

```
我们会发现a和b的值根本没有进行交换，因为c语言在调用函数时，永远只能传递值给函数。而a和b本身不变  
每一个函数有自己所在的变量空间，参数也位于这个独立空间中，和其他函数没有关系，函数里是形式参数，调用时是实际参数，但容易让新学者误解，实参是实际计算的参数，误会调用函数时把变量而不是值传进去。参数和值的关系。  
- **本地变量**  
函数每次运行，就会产生一个独立的变量空间，在这个空间类的变量是函数这次运行所独有的，称作本地变量。定义在函数内部的变量就是本地变量，参数也是本地变量。  
- **变量的生存期和作用域**  
生存期：变量出现和消亡  
作用域：在什么范围内可以访问这个变量  
对于本地变量，这个统一是大括号，块  
本地变量可以在函数的块内，也可以在语句的块内  
```
if(a>b){
    int i = 10;
}

i ++
i会显示未定义，因为其作用域在if块内
```
甚至可以随意拉一个大括号，依附于块。  
块外面定义的变量，在块里面仍然存在。如果块里面有同名的，会掩盖。
同一个块内不能定义同名的变量  
本地变量不会被默认初始化。参数在进入函数时会初始化
- **void**  
void f(void)明确地告诉函数不接受参数  
void f() 表示参数表未知，不表示没有参数，但最好不要这样，因为可能出错。  
- **关于main**  
int main()也是一个函数，int main(void)  
return 0;有意义， windows: if error level 1; unix bash:echo $?; 
- **二维数组**  
int a[3][5]  
通常理解称3行5列的矩阵  
```
for(i=o;i<3;i++){
    for(j=0;j<5;j++){
        a[i][j] = i*j;
    }
}
```
a[i,j] 逗号运算符，i,j计算的结果是j  
- **二维数组的初始化**  
```
int a[][5]{
    {1,2,3,4,5},
    {2,3,4,5,6},
}
```
初始化列数必须给出，行数可以由编译器来数  
每行一个{}，逗号分隔  
最后的逗号可以存在，古老的传统  
如果省略，表示补零  
也可以用定位
- **数组的集成初始化**  
```
int a[] = {2,4,6,7,8,89,5,4,3,3};
int a[13] ={2}
//第一个单元为2，下面的单元全部默认为0
int a[10] = {[0]=2,[2]=3,6}
//给指定的位置赋值，没有定位的数据接在前面数据后面，初始化数据稀疏，只在c99中有效
```
sizeof给出整个数组所占据内容的大小，单位是字节
```
sizeof(a)/sizeof(a[0])
//整个数组的字节除以单个元素的字节
```
- **数组的赋值**  
数组变量本身不能被赋值，要将元素交给另外一个数组必须采用遍历  
数组作为函数的参数时，往往必须再用另一个参数来传入数组的大小，不能在[]中给出数组的大小，不能用sizeof计算元素的个数
```
#include <stdio.h>
int search(int key,int a[],int length );

int main(void){
    int a[]={1,4,5,67,8,6,3,7,84,111};
    int x;
    int loc;
    printf("请输入一个数字：");
    scanf("%d",&x);
    loc = search(x,a,sizeof(a)/sizeof(a[0]));
    if(loc != -1){
        printf("%d在数组的%d位置上\n",x,loc);
    }else{
        printf("%d不在数组中\n",x);
    }
    return 0;
}

int search(int key,int a[], int length){
    int ret = -1;
    int i;
    for(i=0;i<length;i++){
        if(a[i]==key){
            ret = i;
            break;
        }
    }
    return ret;
}

```
- **库函数的手册**  
man sqrt
```
//素数表查找，删除倍数法
#include <stdio.h>
#define maxNumber 25
int main(){
    int x;
    int i;
    int isPrime[maxNumber];
    for(x=0;x<maxNumber;x++){
        isPrime[x] = 1;
    }
    for(i=2;i<maxNumber;i++){
        if(isPrime[i]){
            for(x=2;x*i<maxNumber;x++){
                isPrime[i*x] = 0;
            }
        }
    }
    for(i=2;i<maxNumber;i++){
        if(isPrime[i]){
            printf("%d\t",i);
        }
    }
    printf("\n");
    return 0;
}
```

- **习题**  
```

以下程序片段的输出结果是：
int m[][3] = {1,4,7,2,5,8,3,6,9,};
int i,j,k=2;
for ( i=0; i<3; i++ ) {
    printf("%d", m[k][i]);
}

369
```
- **搜索：线性搜索**  
基本方法：遍历  
```
#include <stdio.h>
struct{
    int amount;
    char *name;
}coins[]={
    {1, "inori"},
    {10, "hotaru"},
    {25, "cocoro"},
    {50, "ayaka"},
};

int main(void){
    int k = 10;
    for(int i=0;i<sizeof(coins)/sizeof(coins[1]);i++){
        if(k ==coins[i].amount){
            printf("%s\n",coins[i].name);
        }
    }
    return 0;
}
```
- **二分搜索**
```
#include <stdio.h>
int search(int k,int a[],int len){
    int left = 0;
    int right = len -1;
    int ret = -1;
    while(right>=left){
        int mid = (left+right)/2;
        if(a[mid]==k){
            ret = mid;
            break;
        }else if(a[mid]>k){
            right = mid-1;
        }else{
            left = mid+1;
        }
    }
    return ret;
}

int main(){
    int a[] = {1,2,3,4,6};
    int k = 6;
    int key = search(k,a,sizeof(a)/sizeof(a[0]));
    printf("%d",key);
    if (key!=-1){
        printf("所找数字在第%d上",key);
    }else{
        printf("查无此数");
    }
    return 0;
}

//注意存在左右相等的情况，因此要大于等于
```
- **选择排序**  
```
#include <stdio.h>
int max(int a[],int len){
    int maxid = 0;
    for(int i=0;i<len;i++){
        if(a[maxid]<a[i]){
            maxid=i;
        }
    }
    return maxid;
}

int main(){
    int a[] = {1,4,57,6,8,9,4,66,73,3};
    int lt = sizeof(a)/sizeof(a[0]);
    for(int i=lt;i>0;i--){
        int maxid = max(a,i);
        int t = a[maxid];
        a[maxid] = a[i-1];
        a[i-1] = t;
    }
    
    for(int i=0;i<lt;i++){
        printf("%d\t",a[i]);
    }
    printf("\n");
    return 0;
}
```