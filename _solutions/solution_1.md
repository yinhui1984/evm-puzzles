```
############
# Puzzle 1 #
############

Bytecode: 3456FDFDFDFDFDFD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='3456FDFDFDFDFDFD5B00'_

00      34      CALLVALUE
01      56      JUMP
02      FD      REVERT
03      FD      REVERT
04      FD      REVERT
05      FD      REVERT
06      FD      REVERT
07      FD      REVERT
08      5B      JUMPDEST
09      00      STOP

? Enter the value to send:
```



## 题解: 

`JUMP` 时需要栈上的值为`0x08`以便跳转到`JUMPDEST`

而栈上的值来自于上一个指令`CALLVAUE` :Get deposited value by the instruction/transaction responsible for this execution

## 答案:

```
? Enter the value to send: 8

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=8&unit=Wei&callData=&codeType=Bytecode&code='3456FDFDFDFDFDFD5B00'_
```



