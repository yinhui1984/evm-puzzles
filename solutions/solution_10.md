```
#############
# Puzzle 10 #
#############

Bytecode: 38349011600857FD5B3661000390061534600A0157FDFDFDFD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='38349011600857FD5B3661000390061534600A0157FDFDFDFD5B00'_

00      38          CODESIZE
01      34          CALLVALUE
02      90          SWAP1
03      11          GT
04      6008        PUSH1 08
06      57          JUMPI
07      FD          REVERT
08      5B          JUMPDEST
09      36          CALLDATASIZE
0A      610003      PUSH2 0003
0D      90          SWAP1
0E      06          MOD
0F      15          ISZERO
10      34          CALLVALUE
11      600A        PUSH1 0A
13      01          ADD
14      57          JUMPI
15      FD          REVERT
16      FD          REVERT
17      FD          REVERT
18      FD          REVERT
19      5B          JUMPDEST
1A      00          STOP

? Enter the value to send: 
? Enter the calldata:
```

## 思路

```
# 00 ~ 06: 如果codesize（0x1B） > msg.value 则跳转到08
00      CODESIZE
01      CALLVALUE
02      SWAP1
03      GT
04      PUSH1 08
06      JUMPI

#07 ~ 0F: calldatasize mod 3 是否为 0 作为跳转条件
07      REVERT
08      JUMPDEST
09      CALLDATASIZE
0A      PUSH2 0003
0D      SWAP1
0E      MOD
0F      ISZERO

#10 ~ 1A: 跳转目标号为(0x19): msg.value + 0x0A
# 所以msg.value = 0x19-0x0A = 0xF (15)
10      CALLVALUE
11      PUSH1 0A
13      ADD
14      JUMPI
15      REVERT
16      REVERT
17      REVERT
18      REVERT
19      JUMPDEST
1A      STOP
```

很简单, 要求 calldatasize mod 3 要为0, 并且直接计算出了msg.value为15



## 答案

```
? Enter the value to send: 15
? Enter the calldata: 0xAABBCC

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=15&unit=Wei&callData=0xAABBCC&codeType=Bytecode&code='38349011600857FD5B3661000390061534600A0157FDFDFDFD5B00'_

? Do you want to play the next puzzle? Yes

All puzzles are solved!
```

