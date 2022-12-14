# EVM PUZZLES SOLUTIONS

Puzzles by fvictorio (https://github.com/fvictorio/evm-puzzles)

## #1

```
CALLVALUE
JUMP
REVERT
REVERT
REVERT
REVERT
REVERT
REVERT
JUMPDEST
STOP
```

Call value puts the amount of wei passed to the contract on the stack and jump pops the top of the stack and jumps to line number, which should be a JUMPDEST. To solve this puzzle, 8 Wei should be passed.

## #2

```
CALLVALUE
CODESIZE
SUB
JUMP
REVERT
REVERT
JUMPDEST
STOP
REVERT
REVERT
```

Call value is subtracted to the value that CODESIZE puts on the stack. CODESIZE puts the number of byte the entire code is onto the stack. The code is 10 bytes so 4 Wei is passed to the contract to complete the puzzle.

## #3

```
CALLDATASIZE
JUMP
REVERT
REVERT
JUMPDEST
STOP
```

CALLDATASIZE puts the amount in bytes of the passed Calldata onto the stack. Calldata of size 4 bytes is passed to solve the puzzle.

## #4

```
CALLVALUE
CODESIZE
XOR
JUMP
REVERT
REVERT
REVERT
REVERT
REVERT
REVERT
JUMPDEST
STOP
```

The XOR of two numbers is calculated by comparing their binary forms. If the bit is the same number then it is turned to 0, else 1. The code size is 12 so to solve this puzzle 6 Wei is passed.

## #5

```
CALLVALUE
DUP1
MUL
PUSH2 0x0100
EQ
PUSH1 0x0C
JUMPI
INVALID
INVALID
JUMPDEST
STOP
INVALID
INVALID
```

The call value is added to the stack and then a duplicate is added to the stack. Those two are multiplied so the square of the call value is what remains on the stack. 256 is then put on top of the stack and then it checks if the top two items on the stack are equal. It returns 1 if they are, else 0. 12 is added to the stack and then JUMPI jumps to the program number of the value of the first item on the stack which is 12 if the second item on the stack is 1. For that to be true the square of the call value must be equal to 256. Therefore 16 Wei is passed to solve the puzzle.

## #6

```
PUSH1 0x00
CALLDATALOAD
JUMP
INVALID
INVALID
INVALID
INVALID
INVALID
INVALID
JUMPDEST
STOP
```

0 is pushed onto the stack then CALLDATALOAD is called which loads the 32 byte calldata value passed with a byte offset of 0. The code then jumps to that value. To solve the puzzle "0x000000000000000000000000000000000000000000000000000000000000000a" is passed as calldata.

## #7

```
CALLDATASIZE
PUSH1 0x00
DUP1
CALLDATACOPY
CALLDATASIZE
PUSH1 0x00
PUSH1 0x00
CREATE
EXTCODESIZE
PUSH1 0x01
EQ
PUSH1 0x13
JUMPI
REVERT
JUMPDEST
STOP
```

The code creates a smart contract with the call data defining the constructor. If the size of the code of the created smart contract is equal to 1 then it jumps over the revert to the end of the code. To complete the puzzle, the size of the smart contract created should be equal to 1 so the call data passed was "0x60016000526001601FF3" .

## #8

```
CALLDATASIZE
PUSH1 0x00
DUP1
CALLDATACOPY
CALLDATASIZE
PUSH1 0x00
PUSH1 0x00
CREATE
PUSH1 0x00
DUP1
DUP1
DUP1
DUP1
SWAP5
GAS
CALL
PUSH1 0x00
EQ
PUSH1 0x1B
JUMPI
REVERT
JUMPDEST
STOP
```

The code creates a smart contract with the call data defining the constructor similar to problem 7. In this case, to get over the revert, the newly deployed contract needs to revert. The call data passed was "0x63600080FD6000526004601CF3". The constructor creates a contract that pushes zero to the stack, duplicates it to act as input for the final opcode which is revert. If a contract reverts when the opcode CALL is used then it returns 0.

## #9

```
CALLDATASIZE
PUSH1 0x03
LT
PUSH1 0x09
JUMPI
REVERT
REVERT
JUMPDEST
CALLVALUE
CALLDATASIZE
MUL
PUSH1 0x08
EQ
PUSH1 0x14
JUMPI
REVERT
JUMPDEST
STOP
```

The code starts by comparing the call data size to 3. If the call data size is greater than three then it is able to jump. Then it multiplies the call value to the call data and compares that to 8. If they are equal then it is able to jump to the end. To solve the puzzle there are two equations, 3 < call data size and call data size \* call value = 8. Solving for both we get call data size = 4 and call value = 2. The call data passed was 0x00000000.

## #10

```
CODESIZE
CALLVALUE
SWAP1
GT
PUSH1 0x08
JUMPI
REVERT
JUMPDEST
CALLDATASIZE
PUSH2 0x0003
SWAP1
MOD
ISZERO
CALLVALUE
PUSH1 0x0A
ADD
JUMPI
REVERT
REVERT
REVERT
REVERT
JUMPDEST
STOP
```

The first jump requires that the code size, which is 27, is greater than the call value. The second jump requires that the call data size modulo 3 be zero and the call value plus 10 be equal to the last jump dest which is 25. We then have 3 equations to solve the puzzle, call value < 27, call data size % 3 = 0, and, call value + 10 = 25. Solving for the call value we get 15 and the call data size can be anything divisible by 3. In this case I used 3.
