Opcode parsing
==============

In any simulator at some point opcodes will have to be parsed in order to determine what code to execute. There are a lot of different solutions to this problem and we will discuss a few of the here and after that explain the solution we chose.

switch statement
----------------

To a lot of simulators out there this is the preferred method. The idea is that you input the opcode or a part of the opcode into a switch statement and continue execution at the matched case. This method has one disadvantage: The case statement can't be generalized to any simulator since the opcodes are (or can be) very different accross different architectures.

Some sort of function array
---------------------------

This isn't used that much at all but for smaller architectures it can be done. The idea is that you have an array of functions that handle an opcode and that you index the array using the opcode. But as mentioned for architectures with a relatively large opcode this array would become far too large and since some instructions have some argument(s) embedded in the opcode a lot of functions appear twice in the array.

Our solution
------------

We wanted to be able to find our instruction in an array, but not have an entry for every possible opcode. So we decided to make masks for opcodes (these masks are then specified in the specification) and before execution of the code match this to an instruction handler. This process (lets call it disassembling) gives the advantage of fast opcode resolution in exchange for a slichtly longer load time. This idea is further illustrated in the following diagram:
