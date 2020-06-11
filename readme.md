#SIMPLE ASSEMBLER && Debugger

Debugger and assembler for [SIMPLE MIPS Reduced](https://github.com/juliancnn/SIMPLE_MIPS_Reduced) processor.
This is just a personal project (the first) to learn go.


##Assembler
###Getting Started
This tool is not interactive
####usage
```shell script
> ./assembler -h                 # Show help
> ./assembler -i filename        # Input file to assemble
> ./assembler -o                 # Output file with binary machine code
> ./assembler -a  "instruction"  # ASM one line, [dont use with -i]
```
Examples
```shell script
./assembler -a  "LUI $R0, 0"
./assembler -i  fire_jump.asm  
./assembler -i  fire_jump.asm -o fire.mem
```

####Features
Instructions are separated by endlines, semicolon is optional
 
 Supports
- Multiline comments (style /*\*multiline comment**/)
- Inline comments (style //*comment*)
- Insensitive instructions
- Register names like $R1 R1 $1 r01
- Tags for jump and banch
- Duplicate tag detection
- Unused tags
- Builtin auto halt at end 
- Builtin nop (sll 0 0 0)

####Instrucction set
Instruction behavior and format (for [SIMPLE MIPS Reduced](https://github.com/juliancnn/SIMPLE_MIPS_Reduced)) is exactly the same as specified in the document
[“MIPS® Architecture for Programmers Volume II-A: The MIPS32® Instruction Set Manual”
(Document Number: MD00086 Revision 6.06 December 15, 2016)](https://s3-eu-west-1.amazonaws.com/downloads-mips/documents/MD00086-2B-MIPS32BIS-AFP-6.06.pdf)

You can find it here https://www.mips.com/products/architectures/mips32-2/

 
|            Type      |    instrucction    |    Usage     |
| :-------------------- | :------------------: |------------------ |
 |Type R|SLL|SLL rd, rt, sa|
 |Type R|SRL|SRL rd, rt, sa|
 |Type R|SRA|SRA rd, rt, sa|
 |Type R|SLLV|SRA rd, rt, rs|
 |Type R|SRLV|SRLV rd, rt, rs|
 |Type R|SRAV|SRAV rd, rt, rs|
 |Type R|ADDU|ADDU rd, rt, rs|
 |Type R|SUBU|SUBU rd, rs, rt|
 |Type R|AND|AND rd, rs, rt|
 |Type R|OR|OR rd, rs, rt|
 |Type R|XOR|XOR rd, rs, rt|
 |Type R|NOR|NOR rd, rs, rt|
 |Type R|SLT|SLT rd, rs, rt|
 |Type I|LB|LB rt, offset (base)|
 |Type I|LH|LH rt, offset (base)|
 |Type I|LW|LW rt, offset (base)|
 |Type I|LWU|LWU rt, offset (base)|
 |Type I|LHU|LHU rt, offset (base)|
 |Type I|LBU|LBU rt, offset (base)|
 |Type I|SB|LB rt, offset (base)|
 |Type I|SH|SH rt, offset (base)|
 |Type I|SW|SW rt, offset (base)|
 |Type I|ADDI|ADDI rt, rs, inmediate|
 |Type I|ANDI|ANDI rt, rs, inmediate|
 |Type I|ORI|ORI rt, rs, inmediate|
 |Type I|XORI|XORI rt, rs, inmediate|
 |Type I|LUI|LUI rt, inmediate|
 |Type I|SLTI|SLTI rt, rs, inmediate|
 |Type I|BEQ|BEQ rs, rt, offset|
 |Type I|BNE|BNE rs, rt, offset|
 |Type I|J|J target|
 |Type I|JAL|JAL target|
 |Type J|JR|JR rs|
 |Type J|JALR|JALR rs (rd=31 default); JALR rd, rs|



##Debbuger
###Getting Started
This tool is interactive
####usage

```shell script
> ./debuger -h                 # Show help
```
#####Params and arguments

|            Flag      | argument type |  default    |    description     |
| :--------------------: | :---| :------------------: |------------------ |
|-d| string |ttyUSB1 | File device in /dev/\<dev\> |
|-b|number|115200 | Baudrate |
|-l|string |*empty*|Mem file to be load (Generated by assembler tool)
|-v| *no argument* | false | verbose mode (serial monitor)

####Prompt command:
| command | usage | description |
| :---    | :--- | :---------- |
| exit | exit | Exit|
|dumprf | dumprf | Gets the 32 values of the general-purpose registers (R0 to R31) |
|step | step *[NUM]* | The processor runs *NUM* clock cycle (default 1)|
|run| run | Run the processor in burst mode|
|pc|pc| Get the PC register |
|reset|reset| Reset pc counter|
|dumpmem|dumpmem *START END* | Dump memory data from *START* to *END* 
|load|load| Loads the specified program with the '-l' option into the processor's program memory|

