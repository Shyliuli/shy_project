shy_project是一个旨在自主实现计算机系统的项目。它由四个主要组成部分构成：shy语言、shyemu模拟器、shy_hardware硬件和shy编译器。shy_project的设计思路是一切皆地址，寄存器，内存，存储，甚至内置指令都使用地址表示。

1. [shy语言](https://github.com/Shyliuli/shy_language)：shy语言类似于汇编语言，是一种低级的编程语言，专注于直接操作底层计算机硬件。使用shy语言可以进行底层编程，包括内存管理、寄存器操作以及其他底层细节。

2. [shyemu模拟器](https://github.com/Shyliuli/shyemu)：shyemu是一个用于运行shy语言程序的模拟器。使用shyemu模拟器，可以在计算机环境中执行shy语言程序，并进行调试和测试。

3. [shy_hardware硬件](https://github.com/Shyliuli/shy_hardware)：shy_hardware是一个专门为运行shy语言而设计的硬件系统。

4. shy编译器：shy编译器是一个用于将shy语言程序转换为可在shy_hardware上执行的机器码的软件工具。它接受shy源代码作为输入，并进行语法解析、优化和转换等过程，生成相应的机器码。

最后，此项目处于新建文件夹阶段，目前正在实现shyemu...
至于shy_hardware...学了数电再说233333


