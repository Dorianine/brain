# 二进制求反
- 将1变成0
- 将0变成1
- 有符号数和无符号数不同，有符号数会导致正负变化，因为最高位是符号位

```c
#include <stdio.h>
int main(){
    int num = 10;
    int num1 = ~num;
    printf("%d\n",num);
    printf("%d\n",num1);

return 0;
}
```
![[Pasted image 20241108132415.png]]
**0000 1010**
**11111 0101**
>对于负数，我们通常使用补码（two's complement）来表示。补码的计算方法如下：
>>首先，找到这个数的反码（one's complement），即将所有的1变为0，所有的0变为1。
>>然后，给反码加1，得到补码。
>>对于`11111 0101`：
>>- 反码是`00000 1010`（将所有的1变为0，所有的0变为1）。
>>- 补码是`00000 1011`（给反码加1）。
>>补码`00000 1011`对应的十进制数是`11`。但是，因为我们最初有一个负数，所以`11111 0101`表示的十进制数是`-11`。
>
>因此，二进制数`11111 0101`在C中表示的有符号整数是`-11`。

# 异或运算`^`
 >[!abstract]  
 >对两个操作数的对应位进行逐位比较，若两个比较的位不同，则结果为1；若相同则结果为0
 
 >[!important]
 >- 异或具有自反性，自己与自己异或结果是0
 >- 异或有交换律，且有结合律
 >- 0与任何数异或是其该数本身
 
>[!example] 
>```c
>#include <stdio.h>
>int main(){
>    int a = 5;
  >  int b = 3;
    >int result = a^b;
    >printf("%d\n",result);
>return 0;
>}
>```
>![[Pasted image 20241108134627.png]]
>**0101**
**0011**
异或后为**0110**即为**6**
==负数也可以进行异或运算==
如-5与5进行异或
**1111   1011**  
**0000 0101**
异或结果为
**1111 1110**补码为**0000 0010**
>即为-2



# 移位运算符
>[!abstract]
>将数值的二进制的每一位向左或向右移动一定位数

>[!caution]
>左移时，右边用0补齐，左边溢出的数字就被discard，
>右移时，无符号整数用0补齐左边，有符号整数用符号位数字补齐左边

>[!example]
>```c
>#include <stdio.h>
>int main()
>{
>chr a=127;
>char b=-128;
>char a1=a<<5;
>char a2=a>>5;
>char b1=b<<5;
>char b2 =b>>5;
>printf("%d %d %d %d",a1,a2,b1,b2);
>return 0;
>}
>```
>返回值为-32 3 0 -4

>[!caution]
>如果将char 类型改成int类型那么就要按32位来，char是8位，不过有时候int是16位

 >[!example]
 >```c
 >#include <stdio.h>
>
>int main()
>
>{
>
>char a=127;
>
>char b=-128;
>
>int a1=a<<5;
>
>int a2=a>>5;
>
>int b1=b<<5;
>
>int b2 =b>>5;
>
>printf("%d %d %d %d",a1,a2,b1,b2);
>
>return 0;
>
>}
 >```
 >结果为4064 3 -4096 -4
 
# 补码
> 为什么要有补码
>- 保持加减法运算规则一致
如**-5+3**=-2
$~$ 1111  1011
$~$ 0000  0011
加起来是1111 1110
1111 1110反码为0000 0001加1即为0000 0010为-2
> - 可以唯一表示0
> - 如-5+5等于1 0000 0000但是那个1是不看的即为0000 0000为0

# 零扩充和符号扩充
>[!abstract]
>将8位整数扩展到32位，把16位扩展到64位等

 >[!attention]
 >零扩充针对非符号数，在左边补0；
 >符号扩充针对符号数，用符号位进行补充

>[!example]
```c
#include <stdio.h>

int main()

{

    unsigned char u8 =0xFA;

    char i8 = 0xFA;

    unsigned int u32 = u8;

    int i32 = i8;

    printf("u32 = %u\n", u32);

    printf("i32 = %d\n", i32);

    return 0;

}
```

# 区别`0x`和`\x`
## `0x`
- **用途：是一个表示16进制整数常量的前缀**
- **语法：`0x`后面跟上16进制数**
- **表示范围：`0x`用于定义数值类型常量，如`int`，`char`，`long`等，表示该值是十六进制格式的**
## `\x`
- **用途：这是给转义字符，用来在字符串中表示十六进制字节，后面可以跟一个或多个十六进制数字，表示该字节的具体值**
- **语法：同`0x`**
>[!note]
>==补充==：
> 二进制的前缀是`0b`,八进制是`0`
>八进制的转义字符是`\`
>==c语言规定==:
>`\`后只能跟三位八进制数字            
>`\x`后只能跟两位16进制数字

>[!example] 
```c
```#include <stdio.h>

int main()

{

    int m=0x1AA;

    printf("%d\n",m); 

    printf("\x42");

    printf("a\x42a\n");//这是不可以的，会认为/x后面跟3给数字，超出范围

    printf("a\x42%c\n",'a');//因为是字符串的一部分，不需要单引号

    printf("a%ca\n",'\x42');//必须有单引号，这是转义字符，是字符！

    printf("a%da",'\x42');//也有单引号!

    return 0;

}

/*输出结果为
426

Ba*

aBa

aBa

a66a
*/
```

# 各种数据类型的大小
![[Pasted image 20241110141810.png]]

# 数组

```c
#include <stdio.h>

int main()

{

    char s[]={'h','e','y'};

    char a[]="hey";

    char b[]={'a'};//双引号可以不加括号，单引号不可以！

    char d[]="a";

    for(int i = 0; i < sizeof(s)/sizeof(s[0]); i++) {

        printf("s[%d] = %c\n", i, s[i]);

    }

  

    for(int i = 0; i < sizeof(a)/sizeof(a[0]) - 1; i++) {

        printf("a[%d] = %c\n", i, a[i]);

    }

  

    printf("b[0] = %c\n", b[0]);

  

    printf("d[0] = %c\n", d[0]);

    printf("%s",a);

    printf("%s",b);

}
}

```


>[!important] 

```c
#include <stdio.h>

int main()

{

    char s[100];

    scanf("%s", &s[0]);

    //等价于scanf("%s", s);数组名是数组首元素的地址

    printf("%s", s);

    char a[]={'a','\0'};

    printf("%s", a);

    return 0;

}

```

> -   `scanf`在敲回车时相当于输入了`\0`
>- 自己创建字符串且不是用“”的时候需要加上斜杠0，否则会出错！因为字符串“hey”本身就已经带了`\0`
>- 只有char类型可以用%s直接输出全部，其他int什么的都要循环输出
```c
char str[6] = {'h', 'e', 'l', 'l', 'o', '\0'};  // 手动加上\0
int a[] = {1, 2, 3, 4, 5};//不需要加\0
```

## 二维数组
```C
short int a[3][4];
```
**则有a[0]  [4]== a[1]  [0]**
![[Pasted image 20241120190922.png]]

# 越界
![[Pasted image 20241124223502.png]]




![[Pasted image 20241124224312.png]]

![[Pasted image 20241124230112.png]]
![[Pasted image 20241124230457.png]]
# 绝对值
- **浮点数** fabs <math.h>
- **整数**abs <stdlib.h>

# 优先级
![[Pasted image 20241201105925.png]]
>**left to right**左结合
>**right to left**右结合
![[Pasted image 20241201111554.png]]
![[Pasted image 20241201111801.png]]![[Pasted image 20241201111826.png]]![[Pasted image 20241201113550.png]]

![[Pasted image 20241201114120.png]]![[Pasted image 20241201120334.png
![[Pasted image 20241201120405.png]]

# 指针
## 指针加减一个整数
![[Pasted image 20241204185929.png]]
![[Pasted image 20241204185929.png]]
![[Pasted image 20241204185805.png]]
## p+i的公式

![[Pasted image 20241204190101.png]]
### 当`*p` 的类型是char，那么p+i就是p+i
## 指针和指针的差
>[! important]
>  不等于地址之差

![[Pasted image 20241204191139.png]]
## 指针作比较

## 指针输出时的扩充问题
![[Pasted image 20241211105612.png]]
![[Pasted image 20241211105715.png]]![[Pasted image 20241211110108.png]]

# 指针和数组
![[Pasted image 20241218153013.png]]![[Pasted image 20241218155217.png]]
![[Pasted image 20241218180841.png]]
![[Pasted image 20241218195320.png]]![[Pasted image 20241218195714.png]]
**puts（a+1)会输出BC\n***
>[!note]
>因为puts里面是地址

**putchar里面不是地址**，putchar（`*a`+3）输出D
![[Pasted image 20241218200034.png]]
![[Pasted image 20241218200340.png]]
**`**a`就是a【0】【0】**

# 命令行参数
![[Pasted image 20241218201419.png]]
# 结构体


![[Pasted image 20241218202909.png]]![[Pasted image 20241218202935.png]]

![[Pasted image 20241218203509.png]]![[Pasted image 20241218203708.png]]
![[Pasted image 20241224135522.png]]
![[Pasted image 20241224145336.png]]![[Pasted image 20241224152738.png]]
![[Pasted image 20241224153153.png]]![[Pasted image 20241224155420.png]]
![[Pasted image 20241224155747.png]]![[Pasted image 20241224155947.png]]
![[Pasted image 20241224185159.png]]
>注意！
>
>**&a是不对的，但是程序跑出来是对的**
# 变量
![[Pasted image 20241228102805.png]]![[Pasted image 20241228102945.png]]
**定义该变量的语句后续不会再被执行！**
**局部变量在所在{}结束后就是死的**
**全局变量和局部静态变量一样，与main同生死**
![[Pasted image 20241228103406.png]]
![[Pasted image 20241228104705.png]]![[Pasted image 20241228105254.png]]
![[Pasted image 20241228105811.png]]
**会报错！**
![[Pasted image 20241228105915.png]]
**欺骗编译器n在外面（其实在里面），这样就不报错了**
![[Pasted image 20241228111812.png]]
![[Pasted image 20241228113936.png]]![[Pasted image 20241228121715.png]]
# 文件
![[Pasted image 20241228133814.png]]![[Pasted image 20241228135738.png]]
![[Pasted image 20241228143443.png]]![[Pasted image 20241228144326.png]]
![[Pasted image 20241228145747.png]]![[Pasted image 20241228150455.png]]