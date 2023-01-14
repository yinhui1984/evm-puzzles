```
############
# Puzzle 2 #
############

Bytecode: 34380356FDFD5B00FDFD

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='34380356FDFD5B00FDFD'_

00      34      CALLVALUE
01      38      CODESIZE
02      03      SUB
03      56      JUMP
04      FD      REVERT
05      FD      REVERT
06      5B      JUMPDEST
07      00      STOP
08      FD      REVERT
09      FD      REVERT

? Enter the value to send:
```

## 题解

`JUMP`时需要跳转到`06`, 所以需要`codesize - callvalue == 6`

当前的`CODESIZE`为10, 所以`callvalue`需要传递4

## 答案

```
? Enter the value to send: 4

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=4&unit=Wei&callData=&codeType=Bytecode&code='34380356FDFD5B00FDFD'_
```



## 注意:

[关于`CODESIZE`](https://www.evm.codes/#38?fork=merge)

Each instruction occupies one byte. In the case of a [PUSH](https://www.evm.codes/#60) instruction, the bytes that need to be pushed are encoded after that, it thus increases the codesize accordingly.

```
// Add some instructions to increase the code size
PUSH29 0
POP

CODESIZE
```

最后栈上的值为`0x20` :

PUSH29 : 一个字节

压入了29个字节的0到栈中, 此时一个30个字节

POP和CODESIZE个一个字节, 所以总共32个字节