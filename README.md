# Kernel-compilation

Install required packeges:
- sudo apt-get install libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf linux-kernel-devel fakeroot kernel-wedge build-essential

Download source code:
- git clone ----- or wget -----
- cd linux-###
-  
Compile with make (with sudo):
- make menuconfig
- make -j 4
- make install
- make modules
- make modules_install
- update-grub

Compile with Clang:
$sudo apt-get isntall clang llvm
$make CC=clang defconfig
$make 
$make modules
$sudo make install
$sudo make modules_install

(wllvm--can extract bc code directly, the following example uses clang11 as an example)
$ sudo apt install clang-11 llvm-11 (if install clang and llvm straightly ,the default version of clang-9&llvm-9 will be installed to ubuntu 20.04)
$ pip install wllvm 
$ sudo cp ~/.local/bin/* /bin 

  $sudo update-alternatives --remove-all clang
  $sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-11 100 
  $sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-11 100

  $clang --version
  $export LLVM_COMPILER=clang
  $make CC=wllvm defconfig
  $make CC=wllvm -j$(nproc) # build Linux kernel with llvm toochain

  $sudo update-alternatives --install /usr/bin/llvm-link llvm-link /usr/bin/llvm-link-11 100
  $extract-bc vmlinux # extract bitcode from vmlinux
  $llvm-dis-11 vmlinux.bc 
  $opt -dot-cfg vmlinux.ll(.bc)  (generate cfg for the compiled kernel
