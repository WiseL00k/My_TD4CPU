| instruction | bit7-bit4 | bit3-bit0 | C | SEL_B | SEL_A | #LOAD0 | #LOAD1 | #LOAD2 | #LOAD3 
|:------------|:---------:|:----------|:-:|:------:|:-----:|:-----:|:------:|:------:|:------:|
|ADD A, Im    |0000       |Im         |X  |   L    |   L   |   L   |   H    |   H   |   H    |
|MOV A, B     |0001       |0000       |X  |   L    |   H   |   L   |   H    |   H   |   H    |
|IN  A        |0010       |0000       |X  |   H    |   L   |   L   |   H    |   H   |   H    |
|MOV A, Im    |0011       |Im         |X  |   H    |   H   |   L   |   H    |   H   |   H    |
|MOV B, A     |0100       |0000       |X  |   L    |   L   |   H   |   L    |   H   |   H    |
|ADD B, Im    |0101       |Im         |X  |   L    |   H   |   H   |   L    |   H   |   H    |
|IN  B        |0110       |0000       |X  |   H    |   L   |   H   |   L    |   H   |   H    |
|MOV B, Im    |0111       |Im         |X  |   H    |   H   |   H   |   L    |   H   |   H    |
|OUT B        |1001       |0000       |X  |   L    |   H   |   H   |   H    |   L   |   H    |
|OUT Im       |1011       |Im         |X  |   H    |   H   |   H   |   H    |   L   |   H    |
|JZ  Im       |1110       |Im         |L  |   H    |   H   |   H   |   H    |   H   |   L    |
|JZ  Im       |1110       |Im         |H  |   X    |   X   |   H   |   H    |   H   |   H    |
|JMP Im       |1111       |Im         |X  |   H    |   H   |   H   |   H    |   H   |   L    |

说明: SEL_B SEL_A 信号用于选择ALU的数据源，#LOAD0-#LOAD3则用于选择ALU的数据终点，说的官方一点，就是  
分别用于控制指令的源操作数和目的操作数。



JMP B	1101 0000



测试加法代码:

0000 0001	ADD A,1	0x01

0100 0000    MOV B, A  0xC0

1001 0000	OUT B		0x90

1111 0000	JMP 0		 0xF0



流水灯代码

0111 0000	MOV B,0	0x70

1001 0000	OUT B		0x90

0111 0001	MOV B,1	0x71

1001 0000	OUT B		0x90

0111 0010	MOV B,2	0x72

1001 0000	OUT B		0x90

0111 0100	MOV B,4	0x74

1001 0000	OUT B		0x90

0111 1000	MOV B,4	0x78

1001 0000	OUT B		0x90

1111 0000	JMP 0		 0xF0



发送1位数据时序

发送0：

OUT 0		1011 0000	0xB0

OUT 4		1011 0100	0xB4

发送1：

OUT 1		1011 0001	0xB1

OUT 4		1011 0101	0xB5



数码管(若1为亮)

显示0:	0011 1111	0x3F



数码管显示数字0：

OUT 1		1011 0011	0xB3

OUT 4		1011 0111	0xB7

OUT 1		1011 0011	0xB3

OUT 4		1011 0111	0xB7

OUT 1		1011 0001	0xB1

OUT 4		1011 0101	0xB5

OUT 1		1011 0001	0xB1

OUT 4		1011 0101	0xB5



数码管(若0为亮)

显示0： 1100 0000	0xC0



