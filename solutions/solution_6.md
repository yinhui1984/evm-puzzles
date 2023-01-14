```
############
# Puzzle 6 #
############

Bytecode: 60003556FDFDFDFDFDFD5B00

Run it in evm.codes: https://www.evm.codes/playground?codeType=Bytecode&code='60003556FDFDFDFDFDFD5B00'_

00      6000      PUSH1 00
02      35        CALLDATALOAD
03      56        JUMP
04      FD        REVERT
05      FD        REVERT
06      FD        REVERT
07      FD        REVERT
08      FD        REVERT
09      FD        REVERT
0A      5B        JUMPDEST
0B      00        STOP

? Enter the calldata:
```

## 题解

`JUMP`需要跳转到`0x0A`, 也就是要求

```
PUSH1 00
CALLDATALOAD
```

执行完成后, 栈顶元素的`0xA`, 也即是 `calldata[0] == A`

> 这里有一个[关于`CALLDATALOAD`](https://www.evm.codes/#35?fork=merge)的一个值得注意的点:
>
> <u>**Stack input**</u>
>
> i: byte offset in the calldata.
>
> <u>**Stack output**</u>
>
> data[i]: 32-byte value starting from the given offset of the calldata. All bytes after the end of the calldata are set to 0.

`CALLDATALOAD`的输出始终是`32`字节, 如果`calldata`不足32字节, 则在末尾补`0`

也就是说如果你输入的calldata为`0x0A`, 那么其在栈上是`a00000000000000000000000000000000000000000000000000000000000000`[查看这里](https://www.evm.codes/playground?fork=merge&unit=Wei&callData=0x0A&codeType=Mnemonic&code='PUSH1%200%5CnCALLDATALOAD'_)

所以, 此处你需要将`calldata`补齐为 `0x000000000000000000000000000000000000000000000000000000000000000a`[查看这里](https://www.evm.codes/playground?fork=merge&unit=Wei&callData=0x000000000000000000000000000000000000000000000000000000000000000a&codeType=Mnemonic&code='PUSH1%200%5CnCALLDATALOAD'_)



## 答案

```
? Enter the calldata: 0x000000000000000000000000000000000000000000000000000000000000000a

Puzzle solved!

Run it in evm.codes: https://www.evm.codes/playground?callValue=0&unit=Wei&callData=0x000000000000000000000000000000000000000000000000000000000000000a&codeType=Bytecode&code='60003556FDFDFDFDFDFD5B00'_
```

