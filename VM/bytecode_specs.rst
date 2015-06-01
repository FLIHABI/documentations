============
Introduction
============

*********
Structure
*********

::

    <hex opcode> <mnemonic> <parameter>[<size of parameter in byte>]

*********
Asterisks
*********

(*) This opcode uses the top of the stack

(**) This operation works on the two first elements on the stack, the first
value on the stack will be the value2 and the next value will be value1. Then
the operation will be "value1 <op> value2"

\+ The elements used are poped

$ A result is pushed on the stack

Multibyte operands are represented in little endian

=============
VM management
=============

- 0x00 halt

=============================
Stack and register management
=============================

- 0x10 save$       <function id>[2]
- 0x11 restore+    <function id>[2]
- 0x12 setr        <register n°>[2]  <constant>[8]
- 0x13 pop(*)+
- 0x17 push$       <constant>[8]
- 0x18 pushr$      <register n°>[2]
- 0x19 popr(*)+    <register n°>[2]

TODO:
save and restore with function id from register

======================
Arithmetic and bitwise
======================

- 0x20 add(**)+$
- 0x21 sub(**)+$
- 0x22 mul(**)+$
- 0x23 div(**)+$
- 0x24 mod(**)+$
- 0x25 and(**)+$
- 0x26 or(**)+$
- 0x27 xor(**)+$
- 0x28 not(*)+$
- 0x29 shr(*)+$ <shift>[1]
- 0x2A shl(*)+$ <shift>[1]

==================
Tests [DEPRECATED]
==================

- 0x30 cmp(**)    Set a flag to {-1, 0, 1}

=========
Branching
=========

- 0x40 call     <symbol n°>[2]
- 0x41 ret
- 0x42 jmp      <offset relative to the next instruction>[2]
- 0x43 je(**)+  <offset relative to the next instruction>[2]
- 0x44 jl(**)+  <offset relative to the next instruction>[2]
- 0x45 jg(**)+  <offset relative to the next instruction>[2]
- 0x46 jne(**)+ <offset relative to the next instruction>[2]
- 0x47 jle(**)+ <offset relative to the next instruction>[2]
- 0x48 jge(**)+ <offset relative to the next instruction>[2]
- 0x49 callr    <register n°>[2]
- 0x4A jmps(*)+

=================
Object management
=================

- 0x50 create(*)+$      pop the member count, push the object id
- 0x51 delete(*)+       pop the object id
- 0x52 read(**)+$       pop the object id, pop the member id, push the value read
- 0x53 write(***)+      pop the object id, pop the member id, pop the value to write

==========================================
[NOT AVAILABLE] Parallel (Working on it !)
==========================================

- 0xA0 parallel_call  <n° symbol>[2] push a task id[4] on the stack
- 0xA1 parallel_wait(*)
