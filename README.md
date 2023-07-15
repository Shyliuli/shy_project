shy_language的整体思路借鉴了x86汇编语言，它由多条命令组成。每个命令的格式如下所示：`add 0x1234 1234`。
其中，第一个部分是内建的系统调用，表示需要执行的操作。第二个和第三个部分是命令的参数。
参数可以分为两种类型：立即数和地址。立即数是具体的数值，而地址表示需要操作的内存地址。

你也可以使用[ox]表示某个地址所指向的内容，根据语法会自动判断此内容为参数还是立即数。

你还可以使用[[ox]]等方式多次套娃（笑）。
下面所有内容中用ox表示地址，num表示立即数，若有多个同类参数，则表示为ox1，ox2或num1，num2

程序在运行前需要通过编译器将指令转换为对应的二进制形式，并将其写入内存。在下面的所有内容中，我们用ox表示一个内存地址，用num表示一个立即数。如果有多个相同类型的参数，则用ox1、ox2或num1、num2来表示它们。

<span id="add">以下是一个示例：</span>

对于指令 `add [0x1234] 1234`，编译器将其转换为二进制形式 `10 12 34 01 04 D2 00`。

其中，`10` 表示 `add` 操作码对应的地址；`12 34` 表示参数一，即内存地址 `0x1234`；`01` 表示参数一是一个指针，需要通过该地址读取其指向的内容；`04 D2` 表示参数二，即立即数 `1234` 的十六进制表示；`00` 表示参数二为一个值，直接使用该值。

在执行指令之前，内存中的状态如下表所示：


| 地址 | 0x1234 | 0x5201 |
| ------ | -------- | -------- |
| 内容 | 0x5201 | 0x0000 |

在执行指令后，内存中的状态如下表所示：


| 地址 | 0x1234 | 0x5201 |
| ------ | -------- | -------- |
| 内容 | 0x5201 | 0x04D2 |

下面是所有内建命令:


| 命令         | 地址 | 命令  | 地址 |
| -------------- | ------ | ------- | ------ |
| [add](#add1) | 0x10 | mov   | 0x18 |
| [sub](#sub)  | 0x11 | reset | 0x19 |
| [sl](@sl)    | 0x12 | cpe   | 0x1A |
| [rl](#rl)    | 0x13 | in    | 0x1B |
| [and](#and)  | 0x14 | out   | 0x1C |
| or           | 0x15 | jmp   | 0x1D |
| xor          | 0x16 | equ   | 0x1E |
| nor          | 0x17 | set   | 0x1F |

#### 1.add

<p id=add1>语法:</p>

`add ox num`

将`ox`指向的内容加上`num`

例子:同[示例](#add)

#### 2.sub

<p id=sub>语法:</p>

`sub ox num`

将`ox`指向的内容减去`num`
例子：运行前
0x0001：0x0099
运行`sub 0x01 0x09`
0x0001：0x0090

#### 3.sl

<p id=sl>语法:</p>

`sl ox num`

将`ox`指向的内容左移`num`位
例子：运行前
0x0001:0x0520
运行`sl 0x01 0x01`
0x0001:0x0A40

#### 4.rl

<p id=rl>语法：</p>

`rl ox num`

将`ox`指向的内容右移`num`位
例子：运行前
0x0001:0x0A40
运行`rl 0x01 0x01`
0x0001:0x0520

#### 5.and

<p id=and>语法：</p>
`and num1 num2`

将`num1`和`num2`进行AND操作，结果保存在寄存器`hx`中。
例子：运行前
0x0001:0x00FF
运行`and 0x01 0xFF`
0x0001:0x0000

#### 6.or

<p id=or>语法：</p>
 `or num1 num2`

将`num1`和`num2`进行OR操作，结果保存在寄存器`hx`中。

例子：运行前
0x0001:0xFFFF
运行``or 0x01 0xFF`
0x0001:0x00FF

#### 7.xor

 <p id=xor>语法：</p>
 `xor num1 num2`

 将`num1`和`num2`进行XOR操作，结果保存在寄存器`hx`中。
 例子：运行前
 	0x0001:0xFF00
    运行`xor 0x01 0xF0F0`
    0x0001:0x0FF0
 
