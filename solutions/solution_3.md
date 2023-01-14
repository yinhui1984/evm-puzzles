```
############
# Puzzle 3 #
############

Bytecode: 3656FDFD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='3656FDFD5B00'_

00      36      CALLDATASIZE
01      56      JUMP
02      FD      REVERT
03      FD      REVERT
04      5B      JUMPDEST
05      00      STOP

? Enter the calldata:
```



## 题解

`JUMP`时需要栈顶的值为`04`以便跳转到`JUMPDEST`

所以, `CALLDTASIZE`压入栈的值应该为`4`, 所以答案为任意4个字节即可

## 答案

```
? Enter the calldata: 0xAABBCCDD

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=0&unit=Wei&callData=0xAABBCCDD&codeType=Bytecode&code='3656FDFD5B00'_
```

