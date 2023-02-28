```
############
# Puzzle 4 #
############

Bytecode: 34381856FDFDFDFDFDFD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='34381856FDFDFDFDFDFD5B00'_

00      34      CALLVALUE
01      38      CODESIZE
02      18      XOR
03      56      JUMP
04      FD      REVERT
05      FD      REVERT
06      FD      REVERT
07      FD      REVERT
08      FD      REVERT
09      FD      REVERT
0A      5B      JUMPDEST
0B      00      STOP

? Enter the value to send:
```

## 题解

要求 `callvalue XOR codesize == 0x0a `

也就是要求  `callvalue XOR 12 == 10` 



## 答案

```
? Enter the value to send: 6

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=6&unit=Wei&callData=&codeType=Bytecode&code='34381856FDFDFDFDFDFD5B00'_
```



