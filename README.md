# EVM PUZZLES SOLUTIONS

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
