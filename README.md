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
