# RISCV Docker Emulator

Provide out of box docker image for the RISCV emulator.

## Precondition

- [Docker](https://www.docker.com/)
- Public network access

## Qemu

### How to Steps

1. Start the docker image with below command
   ```
   docker run -ti plincar/riscv-qemu-emulator:latest
   ```
2. Wait until RISCV ubuntu image boot, and login with `ubuntu:ubuntu`.

   > Note:
   > The ubuntu system may require you change the password for first login.

3. Update package and install toolchain.
   ```
   sudo apt update
   sudo apt install gcc -y
   sudo apt install golang-go -y
   ```
4. Validate the C programming language with the emulator.

   1. Compile below C code with `riscv64-linux-gnu-gcc main.c -o c.out`.

      ```c
      #include <stdio.h>

      int main()
      {
      	printf("Hello, world!\n");
      	return 0;
      }
      ```

   2. If everything goes well, you may see similar output from your terminal.
      ```
      riscv64-linux-gnu-gcc main.c -o c.out
      ./c.out
      Hello, world!
      file c.out
      c.out: ELF 64-bit LSB pie executable, UCB RISC-V, RVC, double-float ABI, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux-riscv64-lp64d.so.1, BuildID[sha1]=b5d550645bc6fbb2045c8b07d710ac9d7df44aad, for GNU/Linux 4.15.0, not stripped
      ```

5. Validate the Golang programming language with the emulator.

   1. Compile below Golang code with `go build -o go.out main.go`.

      ```golang
      package main

      import "fmt"

      func main() {
      	fmt.Println("Hello, world!")
      }
      ```

   2. If everything goes well, you may see similar output from your terminal.
      ```shell
      go build -o go.out main.go
      ./go.out
      Hello, world!
      file go.out
      go.out: ELF 64-bit LSB executable, UCB RISC-V, double-float ABI, version 1 (SYSV), statically linked, Go BuildID=XdPV_KgaapQAF-7BJps-/JfxOKsmko9eaB0VUSH5r/WPPni_yjw6hJogCIMxRZ/xx6PLTsSTbmjFPmeY9eq, not stripped
      ```

### Emulated RISCV CPU

1. From `lscpu`.
   ```shell
   Architecture:          riscv64
   Byte Order:          Little Endian
   CPU(s):                4
   	On-line CPU(s) list: 0-3
   NUMA:
   	NUMA node(s):        1
   	NUMA node0 CPU(s):   0-3
   ```
2. From `cpuinfo`.

   ```
   processor       : 0
   hart            : 3
   isa             : rv64imafdcsu
   mmu             : sv48

   processor       : 1
   hart            : 0
   isa             : rv64imafdcsu
   mmu             : sv48

   processor       : 2
   hart            : 1
   isa             : rv64imafdcsu
   mmu             : sv48

   processor       : 3
   hart            : 2
   isa             : rv64imafdcsu
   mmu             : sv48
   ```

### Open Issues

1. The performance of this emulator is not as fast as hardware due to qemu emulation.

## Reference Link

- [RISC-V Ubuntu Wiki](https://wiki.ubuntu.com/RISC-V?_ga=2.73233749.77592446.1660812353-217946006.1660812353)
- [Docker Hub for Emulator](https://hub.docker.com/r/plincar/riscv-qemu-emulator)
