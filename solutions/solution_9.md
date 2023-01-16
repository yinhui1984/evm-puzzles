```
############
# Puzzle 9 #
############

Bytecode: 36600310600957FDFD5B343602600814601457FD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='36600310600957FDFD5B343602600814601457FD5B00'_

00      36        CALLDATASIZE
01      6003      PUSH1 03
03      10        LT
04      6009      PUSH1 09
06      57        JUMPI
07      FD        REVERT
08      FD        REVERT
09      5B        JUMPDEST
0A      34        CALLVALUE
0B      36        CALLDATASIZE
0C      02        MUL
0D      6008      PUSH1 08
0F      14        EQ
10      6014      PUSH1 14
12      57        JUMPI
13      FD        REVERT
14      5B        JUMPDEST
15      00        STOP

? Enter the value to send: 
? Enter the calldata: 
```

## 思路

```

# 00 ~ 09：  3 小于 sizeof(calldata), 则跳转到09
00     CALLDATASIZE
01     PUSH1 03
03     LT
04     PUSH1 09
06     JUMPI
07     REVERT
08     REVERT
09     JUMPDEST

#0A ~ 0F: msg.value 乘以 sizeof(calldata) 是否等于8
0A     CALLVALUE
0B     CALLDATASIZE
0C     MUL
0D     PUSH1 08
0F     EQ

# 10 ~ 15: 如果上面的EQ返回true， 则跳转到14
10     PUSH1 14
12     JUMPI
13     REVERT
14     JUMPDEST
15     STOP
```

很简单, 题目要求msg.value 乘以 sizeof(calldata) 等于8



## 答案

```
? Enter the value to send: 2
? Enter the calldata: 0xAABBCCDD

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=2&unit=Wei&callData=0xAABBCCDD&codeType=Bytecode&code='36600310600957FDFD5B343602600814601457FD5B00'_

```

