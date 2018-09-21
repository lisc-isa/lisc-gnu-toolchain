# lisc-gnu-toolchain
LISC指令系统是在RISC-V指令系统基础上开发的全新指令系统，具有以下特点：
  1. 16个系统寄存器；
  2. 全新的指令编码；
  3. 大多数指令包含3-4比特的CLIPS位（Cross-Layer Information Parcels），在指令系统中不定义，用于未来定制指令系统之用；
  4. 去除‘JAL’指令的Rd位域，由INSN[28]=1定义PC+4回写，回写地址固定为x1 （去除RISC-V中回写x5的abi）；INSN[28]=0时，不回写，汇编助记符为'J'；
  5. ‘JALR’指令，由INSN[28]=1定义PC+4回写到Rd寄存器；INSN[28]=0时，不回写，汇编助记符为'Jr'；
  6. LISC指令系统的16位指令完全采用RV32E指令编码。
  TODO:
  7. 加入LPTR和SPTR指令，支持指针类型数据的load/store.

LISC指令系统用于北京大学信息科学技术学院《数字逻辑和微处理器设计》课程的教学之用，也向外界全面开放。参见LICENSE文件。

lisc-gnu-toolchian采用主流的RISC-V工具链[https://github.com/riscv/riscv-gnu-toolchain](https://github.com/riscv/riscv-gnu-toolchain) ,更改了其中binutils的若干文件而成。

整个安装过程如下：

    git clone https://github.com/lisc-isa/lisc-gnu-toolchain.git
    cd lisc-gnu-toolchain
    git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
    cd riscv-gnu-toolchain
    patch -p1 < ../0001-mainstream-RVE.patch
    ./configure --prefix=/your/gccinstallpath --with-arch=rv32e --with-abi=ilp32e
    make -j9
