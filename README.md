## xv6-riscv

xv6 is a re-implementation of Dennis Ritchie's and Ken Thompson's Unix
Version 6 (v6).  xv6 loosely follows the structure and style of v6,
but is implemented for a modern RISC-V multiprocessor using ANSI C.

## BUILDING AND RUNNING XV6

You will need a RISC-V "newlib" tool chain from
https://github.com/riscv/riscv-gnu-toolchain, and qemu compiled for
riscv64-softmmu.  Once they are installed, and in your shell
search path, you can run "make qemu".

## Since documentation for setup sucks....

### Building riscv64-unknown-elf-gcc from source

Note: it takes awhile to download and build the source code for the toolchain.

```shell
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
cd riscv-gnu-toolchain
./configure --prefix=/opt/riscv
make -j$(nproc)
sudo chown -R $(whoami):$(whoami) /opt/riscv
nano ~/.bashrc
```

Then add `export PATH=/opt/riscv/bin:$PATH` to `.bashrc`, save/close, and run `source ~/.bashrc`.

Finally, modify the `Makefile` to include the tool definition. CHange the line

```shell
#TOOLPREFIX
```

to

```shell
TOOLPREFIX = riscv64-unknown-elf-
```

### Building QEMU for RISCV from source

```shell
git clone https://gitlab.com/qemu-project/qemu.git
cd qemu
pip install tomli
./configure --target-list=riscv64-softmmu,riscv64-linux-user --prefix=$HOME/qemu-riscv
make -j$(nproc)
make install
nano ~/.bashrc
```

Then add `export PATH=$HOME/qemu-riscv/bin:$PATH` to `.bashrc`, save/close, and run `source ~/.bashrc`.

### Building and running xv6-riscv

Simply run `make qemu` in the root of the project.

To quit xv6-riscv in QEMU, press `Ctrl` and `a` at the same time, release, then hit `x`.
