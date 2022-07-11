# EON Cpu

This is the official **EON** Cpu specification. EON is a simple 16/32/64 bits cpu invented by me. It's a RISC design
with register to register operations and explicit load/store.

# Visible Arquitecture

* 16 general purpose registers of 16/32/64 bits
* register 14 is link register
* register 15 is SP or ZERO
* no branch delay slots

# Opcode map
An opcode takes up to three 16 bit words. The PC internal register points to the next instruction. PC register always points to a even address.
This table show the mapping:

```
  FEDC BA98 7654 3210 IMM       0     1       2     3     4     5     6     7      8       9      A      B     C      D  E   F`
  =================================================================================================================================`
  0000 rd-- rz-- op--           _ zext1   zext2 zext4 bswap sext1 sext2 sext4  csetz  csetnz  csetn csetnn csetp csetnp in out
  0000 sp-- rs-- op-- #-#    jmpr  jalr       _     _ istat  tlba  tlbv     _   get#    set# leasp#   sor#  li##  lea##  _   _
  0000 sp-- sp-- op-- #-# illegal   nop syscall  wait  iret  sret  eret   tlb enter# signal#      _      _ jmp##  jal##  _   _
  0001 rd-- rs-- op-- i16     ld1  ld1i     ld2  ld2i   ld4  ld4i   ld8     _    st1     st2    st4    st8     _      _  _ cas
  0010 rz-- rz-- op-- i16     beq   bne     blt  blti   ble  blei  bltf  blef      _       _      _      _     _      _  _   _
  0011 rd-- rz-- op-- i16       _     _       _     _   add   sub   mul   div    and      or    xor    shl   shr   shri  _   _
  op-- rd-- rz-- rs--           _     _       _     _   add   sub   mul   div    and      or    xor    shl   shr   shri  _   _
```

* **rd** is a destination register, or pointer register in store operations
* **rs** is a source register
* **rz** is a source register, or 0 if SP
* **sp** is stack pointer (SP)
* **op** is a 4 bit opcode
* **`_`** is a unmapped opcode
* **i16** is a signed 16 bit literal
* ` #` i16 is a 16 signed bit literal
* `##` i32 is a 32 signed bit literal
