```
############
# Puzzle 5 #
############

Bytecode: 34800261010014600C57FDFD5B00FDFD

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='34800261010014600C57FDFD5B00FDFD'_

00      34          CALLVALUE
01      80          DUP1
02      02          MUL
03      610100      PUSH2 0100
06      14          EQ
07      600C        PUSH1 0C
09      57          JUMPI
0A      FD          REVERT
0B      FD          REVERT
0C      5B          JUMPDEST
0D      00          STOP
0E      FD          REVERT
0F      FD          REVERT

? Enter the value to send
```

## 题解

`JUMPI`需要跳转到`0x0c`的`JUMPDEST`, 就需要执行到`JUMPI`时, 栈上最顶端的两个元素应该是

```
                 ┌───────────┐
  stack top───▶  │    0xC    │
                 ├───────────┤
                 │    0x1    │
                 ├───────────┤
                 │    ...    │
                 └───────────┘
```

继续往上回退,  则要求

```
CALLVALUE
DUP1
MUL
PUSH2 0100
EQ
```

的执行结果为1(`true`)

也就是`callvalue * callvaue == 0x100` :   x^2=256 ,  x为16

注: `msg.value`为10进制



## 答案

```
? Enter the value to send: 16

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=16&unit=Wei&callData=&codeType=Bytecode&code='34800261010014600C57FDFD5B00FDFD'_
```

