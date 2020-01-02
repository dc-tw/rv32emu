# RISC-V RV32I[MA] emulator with ELF support

Emulator was originally created by Fabrice Bellard and then modified and shared on Hackaday by Frank Buss
as a single C-file. Shaos added some additional statistics and macros.

Requires libelf-dev:
```shell
$ sudo apt-get install libelf-dev
```

How to compile it:
```shell
$ gcc -O3 -Wall -lelf emu-rv32i.c -o emu-rv32i
```
or
```shell
$ make emu-rv32i
```

Passed RV32I compliance tests from https://github.com/riscv/riscv-compliance
- Must install the [risc-v toolchain](https://xpack.github.io/riscv-none-embed-gcc/)
```shell
$ make RISCV_TARGET=spike RISCV_DEVICE=rv32i TARGET_SIM=/full/path/emulator variant
```

Compiling and running simple code:
```shell
$ make test1
```

then
```shell
$ ./emu-rv32i test1
Hello RISC-V!
```

Passed RV32C compliance tests from https://github.com/riscv/riscv-compliance
``shell
make C-ADDI.log
```
If there is no accident, it will output the `TEST PASSED`


RV32M and RV32A instructions may be enabled by commenting `#define STRICT_RV32I`.

## How to build RISC-V toolchain from scratch

https://github.com/riscv/riscv-gnu-toolchain

64-bit universal version (riscv64-unknown-elf-* that can build 32-bit code too):
```shell
$ ./configure --prefix=/opt/riscv
$ make
```

32-bit version (riscv32-unknown-elf-*):
```shell
$ ./configure --prefix=/opt/riscv32 --with-arch=rv32i --with-abi=ilp32
$ make
```
