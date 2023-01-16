```
############
# Puzzle 8 #
############

Bytecode: 36600080373660006000F0600080808080945AF1600014601B57FD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='36600080373660006000F0600080808080945AF1600014601B57FD5B00'_

00      36        CALLDATASIZE
01      6000      PUSH1 00
03      80        DUP1
04      37        CALLDATACOPY
05      36        CALLDATASIZE
06      6000      PUSH1 00
08      6000      PUSH1 00
0A      F0        CREATE
0B      6000      PUSH1 00
0D      80        DUP1
0E      80        DUP1
0F      80        DUP1
10      80        DUP1
11      94        SWAP5
12      5A        GAS
13      F1        CALL
14      6000      PUSH1 00
16      14        EQ
17      601B      PUSH1 1B
19      57        JUMPI
1A      FD        REVERT
1B      5B        JUMPDEST
1C      00        STOP

? Enter the calldata:
```



## 思路

```
//00 ~ 04:  将calldata复制到内存
00    CALLDATASIZE
01    PUSH1 00
03    DUP1
04    CALLDATACOPY

//04 ~ 0A: 使用calldata作为新地址的初始化代码进行初始化
05    CALLDATASIZE
06    PUSH1 00
08    PUSH1 00
0A    CREATE

//0B ~ 13: 调用新地址的rutimecode
0B    PUSH1 00
0D    DUP1
0E    DUP1
0F    DUP1
10    DUP1
11    SWAP5
12    GAS
13    CALL

//14 ~ 1C: 比较CALL的返回值（不是被调用函数的返回值）是否为0（失败），如果为0则成功跳转
14    PUSH1 00
16    EQ
17    PUSH1 1B
19    JUMPI
1A    REVERT
1B    JUMPDEST
1C    STOP
```

所以,与 [puzzle_7](https://github.com/yinhui1984/evm-puzzles/blob/master/solutions/solution_7.md) 一样, 需要手动写一段代码: 它是新地址的creation code, 它将返回一段代码作为新地址的rutime code, 并且要求[CALL](https://www.evm.codes/#f1?fork=merge)(new_address, gas, 0, 0, 0, 0)调用时被revert.

那么, 新地址上的runtime code, 就[使用 `INVALID`](https://www.evm.codes/#fe?fork=merge),  保证100%失败

那么create code 可以写成:

```
//OxFE:相对于REVERT 0 0 
PUSH1 0xFE
PUSH1 0
MSTORE
PUSH1 1
//注意这里的PUSH1 31（十进制），因为MSTORE时，0xFE被补充为32字节了：0x0000.....00FE
PUSH1 31
//返回runtime code:FE
RETURN
```

翻译成bytecode为: `0x60fe6000526001601ff3`



## 答案

```
? Enter the calldata: 0x60fe6000526001601ff3

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=0&unit=Wei&callData=0x60fe6000526001601ff3&codeType=Bytecode&code='36600080373660006000F0600080808080945AF1600014601B57FD5B00'_

```

