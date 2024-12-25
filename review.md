# 期末复习
[Markdown语法大全](https://blog.csdn.net/m0_37367981/article/details/144615486)

## Week13

### HW13

## Week14

### HW14
!!! example True or False  1-5
    `#define PI 3.1415926 `是一条C语句。
    
    - [ ] T  
    - [x] F 

!!! example True or False  1-6
    宏定义不存在类型问题，宏名无类型，它的参数也无类型。
    
    - [x] T  
    - [ ] F  

!!! example Multiple Choice 2-2
    凡是函数中未指定存储类别的局部变量，其隐含的存储类型为(  )
    - [x] A. auto 自动
    - [ ] B. static 静态
    - [ ] C. extern 外部
    - [ ] D. register 寄存器

!!! note 存储变量类型分类
    <details><summary> 点击展开 </summary>
    
    **1.自动变量 auto**

    函数中所有的非静态局部变量、程序中默认的变量都是auto自动变量。
    例如:`int num = 100;`
    num就是一个自动变量,auto是可以省略的
    但只限于C语言中,C++中不能加auto.
    C语言中,`int num = 100; `和 `auto int num = 100;`是相同的
    C++中`auto int num = 100`会报错。

    **2.静态变量 static**

    - 局部静态变量
    
    静态变量在整个程序生命周期中只拷贝一份，如果某函数内的静态变量被访问并且值发生了改变，那么他就会保存新的值。
    - 全局静态变量
    
    定义在最前面的`static int num = 100;`
    在代码中任何地方都可以访问到，而局部静态变量只能在定义他的函数或者块中才能访问到.
    
    **3.外部变量 extern**

    把全局变量在其他源文件中声明成extern 变量，可以扩展该全局变量的作用域至声明的那个文件，其本质作用就是对全局变量作用域的扩展。

    假设有文件aa.c
    ```c
    #include<stdio.h>
    int num = 100;
    ```
    有文件bb.c
    ```c
    #include<stdio.h>
    #include<stdlib.h>
    extern int num;
    int main(){
        printf("%d\n",num);
    }
    ```
    输出: 100 
    将变量num声明成外部变量extern，可以将num的作用域拓展至bbb.c文件中。

    **4.寄存器变量 register**

    寄存器是CPU上面的一个挂件，运行速度很快，一般用在某些常被访问的变量上，将该变量设置为寄存器变量存储在寄存器中方便CPU使用。即某个变量如果一直要被CPU使用的话，存储在寄存器中要比存储在内存中读取起来快的多。
    <mark>注意点1:</mark>
    例如：·`register int num = 100;`
    num被声明成一个寄存器变量，其保存在寄存器中是打印不出地址的&num，但是如果使用`printf(“ox%p”,&num);`打印其地址的，就会变成普通的auto变量。
    <mark>注意点2:</mark>
    寄存器变量不能定义到全局变量位置
    
!!! example Multiple Choice 2-8
    以下是一个C语言程序的除标准库之外的全部源代码，则说法正确的是：

    ```c
    #include <stdio.h>
    extern int k;
    int main() {
        k = 2223;
        printf("%d\n", k);
        return 0;
    }
    ```
    - [ ] **A**. 这段程序编译错误。
    - [x] **B**. 这段程序编译正确，但是链接（link）错误。
    - [ ] **C**. 这段程序编译、链接正确，但是运行时错误。 
    - [ ] **D**. 程序无错，可正常运行。

    **解析**：
    `extern` 关键字表示变量 `k` 是一个外部声明，程序假设变量 `k` 已在其他地方定义（通常在另一个源文件中）。
    但在当前代码中，并没有提供变量 `k` 的定义，因此在编译阶段不会报错，但在链接（linking）阶段会出错，因为链接器找不到 `k` 的实际定义。


!!! example Multiple Choice 2-11
    有如下多文件组织：
    ### **header.h**
    ```c
    #ifndef _HEADER_H
    #define _HEADER_H
    char school[] = "Sanben";
    void fun(char* s);
    #endif
    ```
    ### **File1.c**
    ```c
    #include "header.h"
    int main()
    {
        fun(school);
        printf("%s", school);
    }
    ```
    ### **File2.c**
    ```c
    #include "header.h"
    #include <string.h>
    void fun(char* s)
    {
        strcpy(s, "Yiben");
        return;
    }
    ```
    程序输出结果为：
    - [ ] A. Sanben  
    - [ ] B. Yiben  
    - [ ] C. 编译错误  
    - [x] D. 链接错误  

    **解析**：
    每个包含 `header.h`的源文件都会认为 `school` 是一个新的变量定义。
    因此，当 `File1.c` 和 `File2.c` 同时包含 `header.h` 后，两个目标文件（`File1.o` 和 `File2.o`）中会各自定义一个 `school` 变量。
    在链接阶段，链接器会发现 `school` 被多次定义，报出链接错误。

!!! example Multiple Choice 2-12
    C语言的全局变量的初始化是在以下哪个阶段完成的：
    - [ ] A.main()函数开始后
    - [ ] B.编译链接的时候
    - [x] C.main()函数开始前
    - [ ] D.第一次用到的时候

    **解析**
    C.全局变量在程序加载到内存时（即在 `main()` 函数执行之前）就会被分配存储空间，并初始化。初始化发生在程序的启动代码（由运行时库完成）执行时，`main()` 函数被调用之前。
    
    B.**编译链接的时候**：编译和链接阶段只是分配变量的**符号表**和**地址信息**，但不会进行初始化。
!!! note  **链接错误（Link Error）**
    <details><summary> 点击展开 </summary>

    连接错误是指程序在**编译成功后**，但在链接阶段（linking）出现的问题。链接错误通常发生在编译器试图将各个目标文件（object files）和库文件结合在一起，生成可执行文件的过程中。此时，如果有未定义或无法解析的符号（如变量、函数等），就会导致链接失败。
    ### **链接的作用**
    编译过程通常分为以下几步：
    1. **预处理（Preprocessing）：** 处理宏定义、头文件等，生成纯C代码。
    2. **编译（Compilation）：** 将源代码（C文件）编译为目标文件（.o 或 .obj）。
    3. **链接（Linking）：** 将多个目标文件和所需的库文件链接在一起，生成最终的可执行文件。

    链接阶段的作用是将各个独立编译的模块（目标文件）及库文件中的符号进行解析，使它们彼此关联，完成程序的整体组装。

    ---

    ### **链接错误的常见原因**
    链接错误通常与以下情况有关：

    1. **未定义的符号（Undefined Reference）：**
    - 变量或函数在某个文件中被声明，但没有实际定义。
    - 示例：
        ```c
        extern int x; // 声明外部变量 x
        int main() {
            x = 10;  // 使用变量 x
            return 0;
        }
        ```
        **错误原因：** `x` 被声明为外部变量，但未在任何地方定义。

    2. **多重定义（Multiple Definition）：**
    - 同一个符号（变量或函数）在多个文件中重复定义。
    - 示例：
        文件 `file1.c`：
        ```c
        int x = 10;
        ```
        文件 `file2.c`：
        ```c
        int x = 20;
        ```
        编译时不会报错，但在链接阶段会出现冲突。

    3. **函数缺失：**
    - 调用了某个函数，但没有提供该函数的实现（定义）。
    - 示例：
        ```c
        void func(); // 声明
        int main() {
            func(); // 调用
            return 0;
        }
        ```
        如果没有提供 `func` 的定义，链接器会报错。

    4. **库文件丢失：**
    - 程序依赖的库文件没有包含在链接过程中。
    - 示例：使用数学库函数 `sin`，但未链接数学库（需要 `-lm`）。

    5. **链接顺序错误：**
    - 在使用静态库时，库的链接顺序不正确会导致符号未解析。
     
!!! note  **编译的四个过程**
    <details><summary> 点击展开 </summary>

    C语言程序从源代码到可执行文件，通常需要经过**四个主要阶段**：**预处理（Preprocessing）**、**编译（Compilation）**、**汇编（Assembly）** 和 **链接（Linking）**。以下是各阶段的详细解释：

    ---

    ### **1. 预处理（Preprocessing）**
    - **主要功能：**
    - 处理源代码中的预处理指令（如 `#include`、`#define` 等）。
    - 删除注释，展开宏，将头文件的内容插入到源代码中。
    - 生成一个**预处理后的源文件**（通常后缀为 `.i` 或 `.ii`）。

    - **关键操作：**
    - **宏替换：** 替换 `#define` 定义的宏，例如：
        ```c
        #define PI 3.14
        printf("%f", PI);  // 替换为 printf("%f", 3.14);
        ```
    - **头文件展开：** 将 `#include` 的头文件内容插入到源文件中。
    - **条件编译：** 根据宏条件判断是否保留某段代码（如 `#ifdef`）。

    - **工具和命令：**
    - 常用的 GCC 命令：`gcc -E main.c -o main.i`

    ---

    ### **2. 编译（Compilation）**
    - **主要功能：**
    - 将预处理后的源代码（`.i` 文件）翻译为**汇编代码**（`.s` 文件）。
    - 检查语法和语义错误。

    - **关键操作：**
    - **语法分析：** 确保代码符合 C 语言语法规则。
    - **语义分析：** 检查变量是否定义、类型是否匹配、函数调用是否正确等。
    - **中间代码生成：** 将代码转换为编译器内部的中间表示（IR）。
    - **优化：** 对代码进行优化（如循环展开、常量折叠等）。
    - **生成汇编代码：** 输出汇编代码文件（`.s` 文件）。

    - **工具和命令：**
    - 常用的 GCC 命令：`gcc -S main.i -o main.s`

    ---

    ### **3. 汇编（Assembly）**
    - **主要功能：**
    - 将汇编代码（`.s` 文件）翻译为**机器代码**，生成目标文件（`.o` 文件）。

    - **关键操作：**
    - 汇编器根据目标平台的指令集，将汇编代码翻译为对应的机器指令。
    - 生成**目标文件**，目标文件中包含机器指令和二进制数据，但并非完整的可执行程序。

    - **工具和命令：**
    - 常用的 GCC 命令：`gcc -c main.s -o main.o`

    ---

    ### **4. 链接（Linking）**
    - **主要功能：**
    - 将多个目标文件（`.o` 文件）和依赖的库文件组合在一起，生成最终的可执行文件。
    - 解析外部符号（如跨文件的函数调用或全局变量引用）。

    - **关键操作：**
    - **符号解析：** 找到所有未定义的符号（如函数或变量的定义）。
    - **地址分配：** 为每个目标文件中的代码和数据分配内存地址。
    - **库文件链接：** 将静态库或动态库的内容与目标文件结合。

    - **工具和命令：**
    - 常用的 GCC 命令：`gcc main.o -o main`

    ---

    ### **四个阶段的总结**
    以下是每个阶段的输入和输出文件的对应关系：

    | 阶段             | 输入文件           | 输出文件        | 命令示例                          |
    |------------------|-------------------|----------------|-----------------------------------|
    | **预处理**       | 源文件（`.c`）    | 预处理文件（`.i`） | `gcc -E main.c -o main.i`        |
    | **编译**         | 预处理文件（`.i`） | 汇编文件（`.s`）  | `gcc -S main.i -o main.s`        |
    | **汇编**         | 汇编文件（`.s`）   | 目标文件（`.o`）  | `gcc -c main.s -o main.o`        |
    | **链接**         | 目标文件（`.o`）   | 可执行文件       | `gcc main.o -o main`             |

    ---

    ### **示例代码的完整编译流程**
    假设源文件是 `main.c`：
    ```c
    #include <stdio.h>
    int main() {
        printf("Hello, World!\n");
        return 0;
    }
    ```

    1. **预处理（`gcc -E main.c -o main.i`）**
    - 输出文件 `main.i`，内容为展开后的代码（头文件和宏替换后）。

    2. **编译（`gcc -S main.i -o main.s`）**
    - 输出文件 `main.s`，内容为汇编代码。

    3. **汇编（`gcc -c main.s -o main.o`）**
    - 输出文件 `main.o`，内容为机器代码的目标文件。

    4. **链接（`gcc main.o -o main`）**
    - 输出文件 `main`，这是最终的可执行文件。

    ---

    ### **注意**
    - **错误检查**：
    - **预处理阶段：** 宏错误或头文件找不到会报错。
    - **编译阶段：** 语法错误、语义错误会在此阶段报错。
    - **汇编阶段：** 汇编代码生成问题会报错（很少见）。
    - **链接阶段：** 外部符号未定义、多重定义等问题会在链接阶段报错。

!!! example Code Completion 6-1 快速幂的实现
    **Quick Power**

    ```c
    int Power(int N, int k){
        int temp=N%MOD,ans=1;
        while(k>0){
            if(k&1) ans=ans*temp%MOD;
            temp=temp*temp%MOD;
            k>>=1;
        }
        return ans%MOD;
    }
    ```

!!! example Programming 7-2 研究：双精度实数的机内码*
    请编写程序，输入十进制双精度实数，输出其 64 位机内码。
    要求：以十六进制形式输出机内码
    Sample Input
    `3.6`
    Sample Output
    `400CCCCCCCCCCCCD`

    Explanation：

    要求：十六进制机内码中的字母均为大写。
    例如：实数 3.6 转换成二进制是 11.1001100110011001...，科学计数法记为：$1.11001100110011001...×2^1$
    因此 64 位的机内码为：0100000000001100110011001100110011001100110011001100110011001101
    用十六进制书写则为：400CCCCCCCCCCCCD

    ```c
    #include<stdio.h>
    int main()
    {
        double num;
        scanf("%lf",&num);
        unsigned char* p=&num;
        for(i=sizeof(num)-1;i>=0;i--) 
        printf("%02X",*(p+i));//%02X 表示输出两位十六进制数，不足两位用0填充
    }
    ```
    **相关资源**
    - [惭愧！直到今天才真正明白为什么int型的取值范围是-2^31~2^31-1](https://blog.csdn.net/wangerxiao121223/article/details/105501006)
    - [int、unsigned int、float、double 和 char 在内存中存储方式](https://blog.csdn.net/itworld123/article/details/78914969)
