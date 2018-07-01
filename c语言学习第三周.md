- **循环控制**  
break;跳出循环  
continue;跳过循环这一轮剩下的语句进入下一轮  
循环的嵌套  
```
#include <stdio.h>
int main(){
    int x;
    int cnts,cntd;
    printf("请输入要查找素数的范围（空格分隔）：");
    scanf("%d %d",&cnts,&cntd);
    for(x=cnts;x<cntd;x++){
        int i;
        int isPrime = 1;
        for(i=2;i<x;i++){
            if(x%i==0){
                isPrime = 0;
                break;
            }
            }
        if (isPrime){
            printf("%d ",x);
        }
    }
    return 0;
}

```  
接力break，我们可以用exit = 1来做控制  
或者使用goto语句，goto语句后面要有一个标号，
```
goto out;
....
out:
```
```
#include <stdio.h>
int main(){
    int x = 10;
    int one,two,five;
    int exit = 0;
    for (one=0; one<x*10; one++) {
        for (two=0;two<x*10/2;two++){
            for(five=0;five<x*10/5;five++){
                if(one+two*2+five*5 ==x){
                    printf("找零%d一角%d二角%d五角\n",one,two,five);
                    exit = 1;
                    break;
                    //goto out;
                }
            }
            if(exit){
                break;
            }
        }
        if(exit){
            break;
        }
    }
//out:
    return 0;
}
```
