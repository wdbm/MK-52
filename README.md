# ELEKTRONIKA MK-52 MICROCALCULATOR

*Will Breaden Madden*

# Introduction

The Elektronika MK-52 is an RPN programmable microcalculator. The MK-52 is one of the most advanced Soviet calculators ever made. The MK-52 was used as a backup for onboard computers of the Soyuz spacecraft mission TM-7 (1988-11-26--1989-04-27) for calculating the docking parameters of Soyuz docking with the Mir space station.

The MK-52 vacuum fluorescent display is quite dim and it is a very slow calculator, but it provides a powerful set of programming functions. The MK-52 is functionally identical to the MK-62, but features an internal non-volatile EEPROM memory module and expansion ports. One of the specific features of the B3-34 -- MK-54 line was a variety of undocumented features, substantially exceeding that of documented features. Some characteristics of the MK-52 as as follows:

|**characteristic**          |**details**                                        |
|----------------------------|---------------------------------------------------|
|type                        |scientific                                         |
|precision                   |8 BCD digits, exponent ±99                         |
|input mode                  |Reverse Polish Notation                            |
|production                  |Kiev, 1983--1991-11                                |
|price                       |115₽                                                                                              |
|volatile memory capacity    |105                                                |
|non-volatile memory capacity|512 kb                                             |
|non-volatile memory type    |EEPROM                                             |
|clock speed                 |455 kHz ceramic resonator                          |
|ROM memory modules' type    |fabric                                             |
|size                        |212 mm * 78 mm * 35 mm                             |
|weight                      |250 g                                              |
|display size                |8 digit manissa, two digit exponent, separate signs|
|display type                |green vacuum fluorescent                           |
|power supply unit           |D2-37                                              |

# Notation

Throughout this documentation, keyboard-key-style boxed characters represent microcalculator keys. For example, <kbd>+</kbd> represents the addition key.

## Some key notations

|**key notation**         |**key appearance**                    |
|-------------------------|--------------------------------------|
|<kbd>CHS</kbd>           |<kbd>/-/</kbd>                        |
|<kbd>EE</kbd>            |<kbd>Бл</kbd>                         |
|<kbd>enter</kbd>         |<kbd>B↑</kbd>                         |
|<kbd>Addr</kbd>          |<kbd>A↑</kbd>                         |
|<kbd>R/W</kbd>           |<kbd>↑↓</kbd>                         |
|<kbd>R/S</kbd>           |<kbd>C/л</kbd>                        |

|**switch notation**      |**switch appearance**                 |
|-------------------------|--------------------------------------|
|clear/read/write         |<kbd>C/З/CЧ</kbd>                     |
|degrees/gradiants/radians|<kbd>Р/ГРД/Г</kbd>                    |
|data/programming         |<kbd>Д/P</kbd>                        |
|automatic/programming    |<kbd>A/П</kbd>                        |

# Modes of operation

The MK-52 has two main operating modes: `automatic mode` and `programming mode`. General calculations and operations are performed in automatic mode; programs are input in programming mode. To switch between modes, one must execute <kbd>F</kbd> <kbd>/-/</kbd> to switch to automatic mode and one must execute <kbd>F</kbd> <kbd>EE</kbd> to switch to programming mode.

# Automatic mode

Basic operations in automatic mode are conducted in accordance with RPN (Reverse Polish Notation) logic. For example, to evaluate 2+3, the following execution is required: 

   <kbd>2</kbd> <kbd>B↑</kbd> <kbd>3</kbd> <kbd>+</kbd>.

# Programming mode

In simple programming, commands are typed into the MK-52 in programming mode and are then executed in order. The MK-52 is fully capable of memory management and both conditional and unconditional branching.

In programming mode, the screen displays information about the program in memory. For example, if

    10 01 0E 03

is displayed, then this means that

- `0E` is stored at program step `00`,
- `01` is stored at program step `01`,
- `10` is stored at program step `02`

and the MK-52 is prompting for data to be input for program step `03`. Individual program operations are represented by two-digit operation codes in programming mode.

    10 01 0E 03

# Memory

The internal volatile memory of the MK-52 has 105 steps. The internal non-volatile EEPROM memory is organised as 1024 4 bit nibbles and can store programs and data. Each program step requires 1 byte (2 nibbles) of memory; each register requires 7 bytes (14 nibbles).

## Writing to non-volatile memory

Before entering a program into volatile memory with the intention of writing this program to non-volatile memory, the non-volatile program space to which the program is to be written must be cleared first, because performing the clearing operation clears the volatile memory as well as the selected area of the non-volatile memory.

Each program step requires 1 byte of memory and each register requires 7 bytes of memory.

When clearing, reading or writing to the non-volatile memory, the "address" and "range" are specified in the form of a six-digit number, preceded by a non-zero number (which is ignored) in automatic mode; i.e., `1aaaadd` corresponds to `dd` bytes, starting at memory address `aaaa`. A two-position data/program switch (<kbd>Д/P</kbd>) controls whether data (from the registers) or program memory is transferred; a three-position switch is used to select `clear`, `read` and `write` operations (<kbd>C/З/CЧ</kbd>).

### Example: Entry of program, writing to and reading from non-volatile memory

This example demonstrates the entry of a program (which simply adds 1 to a user input number and then displays the result) and the writing and reading of this program to and from non-volatile memory. The program is four steps long and, hence, requires 4 bytes of EEPROM memory.


- [Step 1] Clear the memory.
    - Switch the <kbd>C/З/CЧ</kbd> switch to <kbd>C</kbd> (clear) and switch the <kbd>Д/P</kbd> switch to <kbd>P</kbd> (program mode).
    - Switch the <kbd>A/П</kbd> switch to <kbd>A</kbd> (automatic mode).
    - Enter `1000004` (4 bytes starting at address `0000`).
    - <kbd>A↑</kbd> (address)
    - <kbd>↑↓</kbd> (R/W)
- [Step 2] Enter the program.
    - Switch the <kbd>C/З/CЧ</kbd> switch to <kbd>CЧ</kbd> (write).
    - Switch the <kbd>Д/P</kbd> switch to <kbd>P</kbd> (program mode).
    - Enter the program.
        - Initially, the screen should display `00`, prompting for input.
        - <kbd>B↑</kbd> (enter)
        - <kbd>1</kbd>
        - <kbd>+</kbd>
        - The screen should display now `10 01 0E 03`.
        - <kbd>C/л</kbd> (R/S)
        - The screen should display now `50 10 01 04`.
        - The program is in volatile memory.
