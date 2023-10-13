# Hack Assembler

The Hack Assembler is a Python program designed to convert assembly code written in the Hack assembly language into machine code, which can be executed on the Hack computer platform.

## Overview

### There is the `NOTICE` section which is important at the end of the script.

The Hack Assembler consists of two main passes: Pass 1 and Pass 2.

**Pass 1:** In this pass, the assembler scans through the input assembly file, generates an intermediate representation for each instruction, and populates a symbol table with predefined symbols and RAM locations. The intermediate representation includes details about each instruction's type, values, operands, and more.

**Pass 2:** In this pass, the assembler processes the intermediate representation generated in Pass 1 and generates the actual machine code. The machine code is generated based on the predefined patterns for the Hack computer's assembly instructions.

## Usage

To use the Hack Assembler, follow these steps:

1. Make sure you have Python installed on your system.

2. Open a terminal or command prompt.

3. Run the assembler script with the name of the input assembly file as an argument:

```bash 
python3 assembler.py input_file.asm
```

Replace `input_file.asm` with the name of your actual assembly file.

4. The assembler will generate machine code based on the input assembly file. If successful, it will also create an output file named `input_file.hack`.

## Files

- `assembler.py`: The main assembler script. It handles both passes and generates the machine code.

## Assembly Language Syntax

The Hack assembly language used with this assembler follows a simplified syntax. Instructions can be written in the following formats:

- A-instructions: `@value` (e.g., `@42`)
- C-instructions: `dest=comp;jump` (e.g., `D=M;JGT`)
- Parenthesized Symbols: `(LABEL)` (e.g., `(LOOP)`)

## Symbols and Labels

The assembler supports predefined symbols like `SP`, `LCL`, `R0` through `R15`, and others, as well as user-defined labels enclosed in parentheses. The symbol table maps symbols to their corresponding RAM addresses.

## Explain `parse()` Function

The parse function in the Hack Assembler is a crucial component responsible for analyzing and processing individual assembly instructions. It breaks down each instruction into its constituent parts, such as the instruction type, destination, computation, jump condition, and more.

### Parameters

- `command`: The assembly instruction to be parsed.
- `add`: The current address of the instruction being parsed.

### Function Logic

The parse function follows a series of steps to analyze the provided assembly instruction:

1. Cleanup: It removes leading and trailing whitespaces, as well as comments.
2. Categorization: It categorizes the instruction into one of the following types: `A-instruction`, `C-instruction`, `Parenthesized Symbol (P)`, or `Undefined`.
3. Instruction Details: Depending on the instruction type, the function extracts relevant information such as values, types, destinations, computations, and jumps.
4. Symbol Handling: For labels and symbols, the function checks if they are present in the symbol table. If not, it assigns them a unique register value.

### Supported Instructions

The parse function supports the following types of instructions:

- A-instruction: An instruction that begins with @ and may represent either a numerical value (NUM) or a symbolic label (SYM).
- C-instruction: An instruction in the form of dest=comp;jump, where the destination, computation, and jump fields are processed.
- Parenthesized Symbol: An instruction enclosed in parentheses, indicating a label.

### Intermediate Representation

The parsed details of each instruction are stored in an intermediate representation (IR) data structure. This IR holds information about the instruction's type, value, value type, destination, computation, jump, and status.

### Error Handling

The function handles various error scenarios, such as undefined or incorrectly formatted instructions, and sets the status accordingly. This allows for graceful handling of these scenarios during the assembly process.

### Usage Example

To demonstrate the parse function's usage, here's how it can be called within the `run_assembler()` function:
```python
def run_assembler(file_name):
    set_inst = []
    with open(file_name, "r") as f:
        add = 0
        for command in f:
            s = parse(command, add)
            if s and s["instruction_type"] != "P":
                add += 1
                set_inst.append(s)
```


## Output

After running the assembler, the generated machine code will be printed in the terminal, and an output `.hack` file will be created with the same name as the input assembly file.

## Example

For a working example, consider using the provided sample assembly code file named `series_sum.asm`. You can run the assembler on this file using the following command:

```bash
python3 assembler.py series_sum.asm
```

After executing, the program provides terminal output for debugging purposes. It prints the filtered assembly (ASM) code, the generated machine code for the `.hack` file, and the updated `symbol_table` that displays new symbols.

Additionally, the program generates the `series_sum.hack` file as an example output.

Below is the terminal output
``` terminal
python3 assembler.py series_sum.asm
Assembling file: series_sum.asm

  0 => @i
  1 => M=1
  2 => @sum
  3 => M=0
  4 => (LOOP)
  4 => @i
  5 => D=M
  6 => @10
  7 => D=D-A
  8 => @END
  9 => D;JGT
 10 => @i
 11 => D=M
 12 => @sum
 13 => M=M+D
 14 => @i
 15 => M=M+1
 16 => @LOOP
 17 => 0;JMP
 18 => (END)
 18 => @END
 19 => 0;JMP
---------------------------
  0 => 0000000000010000
  1 => 1110111111001000
  2 => 0000000000010001
  3 => 1110101010001000
  4 => 0000000000010000
  5 => 1111110000010000
  6 => 0000000000001010
  7 => 1110010011010000
  8 => 0000000000010010
  9 => 1110001100000001
 10 => 0000000000010000
 11 => 1111110000010000
 12 => 0000000000010001
 13 => 1111000010001000
 14 => 0000000000010000
 15 => 1111110111001000
 16 => 0000000000000100
 17 => 1110101010000111
 18 => 0000000000010010
 19 => 1110101010000111
---------------------------
i                    => 16
sum                  => 17
LOOP                 => 4
END                  => 18

Machine code generated successfully
Writing output to file: series_sum.hack
```

## NOTICE

After comparing series_sum.hack (or any .hack files) that the program produce with the `Assemble.bat` program from `nand2tetris` project, the `diff` and `cmp` (or more compared tools) always show the difference while the bits represent for the instruction are the same for both two file. The reason is reasonable since we use `hexdump` to see each byte in the `.hack` file.

Consider `series_sum.hack` is from `assembler.py` while the `series_sum1.hack` is from `Assemble.bat`, we have these tables:

```terminal
> hexdump series_sum.hack
0000000 3030 3030 3030 3030 3030 3130 3030 3030
0000010 310a 3131 3130 3131 3131 3031 3130 3030
0000020 0a30 3030 3030 3030 3030 3030 3130 3030
0000030 3130 310a 3131 3130 3130 3130 3030 3130
0000040 3030 0a30 3030 3030 3030 3030 3030 3130
0000050 3030 3030 310a 3131 3131 3031 3030 3030
0000060 3031 3030 0a30 3030 3030 3030 3030 3030
0000070 3030 3031 3031 310a 3131 3030 3031 3130
0000080 3031 3031 3030 0a30 3030 3030 3030 3030
0000090 3030 3130 3030 3031 310a 3131 3030 3130
00000a0 3031 3030 3030 3030 0a31 3030 3030 3030
00000b0 3030 3030 3130 3030 3030 310a 3131 3131
00000c0 3031 3030 3030 3031 3030 0a30 3030 3030
00000d0 3030 3030 3030 3130 3030 3130 310a 3131
00000e0 3031 3030 3130 3030 3130 3030 0a30 3030
00000f0 3030 3030 3030 3030 3130 3030 3030 310a
0000100 3131 3131 3031 3131 3031 3130 3030 0a30
0000110 3030 3030 3030 3030 3030 3030 3130 3030
0000120 310a 3131 3130 3130 3130 3030 3030 3131
0000130 0a31 3030 3030 3030 3030 3030 3130 3030
0000140 3031 310a 3131 3130 3130 3130 3030 3030
0000150 3131 0a31
0000154
> hexdump series_sum1.hack
0000000 3030 3030 3030 3030 3030 3130 3030 3030
0000010 0a0d 3131 3031 3131 3131 3131 3030 3031
0000020 3030 0a0d 3030 3030 3030 3030 3030 3130
0000030 3030 3130 0a0d 3131 3031 3031 3031 3031
0000040 3030 3031 3030 0a0d 3030 3030 3030 3030
0000050 3030 3130 3030 3030 0a0d 3131 3131 3131
0000060 3030 3030 3130 3030 3030 0a0d 3030 3030
0000070 3030 3030 3030 3030 3031 3031 0a0d 3131
0000080 3031 3130 3030 3131 3130 3030 3030 0a0d
0000090 3030 3030 3030 3030 3030 3130 3030 3031
00000a0 0a0d 3131 3031 3030 3131 3030 3030 3030
00000b0 3130 0a0d 3030 3030 3030 3030 3030 3130
00000c0 3030 3030 0a0d 3131 3131 3131 3030 3030
00000d0 3130 3030 3030 0a0d 3030 3030 3030 3030
00000e0 3030 3130 3030 3130 0a0d 3131 3131 3030
00000f0 3030 3031 3030 3031 3030 0a0d 3030 3030
0000100 3030 3030 3030 3130 3030 3030 0a0d 3131
0000110 3131 3131 3130 3131 3030 3031 3030 0a0d
0000120 3030 3030 3030 3030 3030 3030 3130 3030
0000130 0a0d 3131 3031 3031 3031 3031 3030 3130
0000140 3131 0a0d 3030 3030 3030 3030 3030 3130
0000150 3030 3031 0a0d 3131 3031 3031 3031 3031
0000160 3030 3130 3131 0a0d
0000168
```

After `ls -l`, we have these piece of information:

```terminal
-rwxrwxrwx 1 340 series_sum.hack
-rwxrwxrwx 1 360 series_sum1.hack
```
As we see, the number of bytes in `series_sum.hack` is less than `series_sum1.hack` has while still perform exactly the same. 

This becaue the `NULL` byte in `series_sum1.hack` occupied (`0a0d`).
