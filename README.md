# EON Cpu

This is the official **EON** Cpu specification. EON is a simple 32/64 bits cpu designed by me. It's a RISC design
with register to register operations and explicit load/store.

I try hard to give it a motorola 68000 feel. It was a pleasure to do m68k assembler programming in the 80's. Maybe I will be able
to retain some of it's spirit so you may also enjoy **EON** assembler programming.

In my account you can find related repositories: an assembler, boot ROM, and some hardware implementations. At page foot there are the relevant links.

# Visible Arquitecture

* 16 general purpose registers of 32/64 bits
* register 14 is link register
* register 15 is SP or ZERO
* no branch delay slots

# Opcode map
An opcode takes up to three 16 bit words. The PC internal register points to the next instruction. PC register always points to an even address.
This table show the mapping:

```
  FEDC BA98 7654 3210 IMM       0     1       2     3     4     5     6     7      8       9      A      B     C      D  E   F
  ===============================================================================================================================
  0000 rd-- rz-- op--           _ zext1   zext2 zext4 bswap sext1 sext2 sext4  csetz  csetnz  csetn csetnn csetp csetnp in   out
  0000 sp-- rs-- op-- #-#    jmpr  jalr       _     _ istat  tlba  tlbv     _   get#    set# leasp#   inv#  li##  lea##  _   _
  0000 sp-- sp-- op-- #-# illegal   nop syscall  wait  iret  sret  eret   tlb enter# signal#      _      _ jmp##  jal##  _   _
  0001 rd-- rs-- op-- i16     ld1  ld1i     ld2  ld2i   ld4  ld4i   ld8     _    st1     st2    st4    st8     _      _  _   cas
  0010 rz-- rz-- op-- i16     beq   bne     blt  blti   ble  blei  bltf  blef      _       _      _      _     _      _  _    _
  0011 rd-- rz-- op-- i16       _     _       _     _   add   sub   mul   div    and      or    xor    shl   shr   shri  _    _
  op-- rd-- rz-- rs--           _     _       _     _   add   sub   mul   div    and      or    xor    shl   shr   shri  imul idiv
```

* **rd** is a destination register, or pointer register in store operations
* **rs** is a source register
* **rz** is a source register, or 0 if SP
* **sp** is stack pointer (SP)
* **op** is a 4 bit opcode
* **`_`** is a unmapped opcode
* **i16** is a signed 16 bit literal
* ` #` is a 16 signed bit literal
* `##` is a 32 signed bit literal

# Links
* [eon classical assembler](https://github.com/elgron-eon/eonasm)
* [eon ROM](https://github.com/elgron-eon/eonrom)
* [eon with arduino and real hardware](https://github.com/elgron-eon/eonduino)
* [eon with tinyfpga BX in verilog](https://github.com/elgron-eon/eonv)
* [eon with esp8266/esp32](https://github.com/elgron-eon/eon-esp32)

