Decompress the img file

`$ cd tools;tar -xvf ./hdc-0.11-new.img.tar.gz`






# Original README

linux-0.11 development environment(linux-based)
	
	miracle <378479645@qq.com>
	update: 2019-8-2

# 1. preparation

* a linux distribution: debian and ubuntu are recommended
* a virtual machine: qemu(recommend) or bochs 
* some tools: cscope, ctags, gcc-4.3(or later), vim, bash, gdb, dd, qemu, xorg-dev, xserver-xorg-dev...
  $ apt-get install qemu cscope exuberant-ctags gcc-4.3 vim-full bash gdb build-essential hex graphviz xorg-dev xserver-xorg-dev vgabios libxpm-dev bochs bochs-x bochsbios bximage
* a linux-0.11 hardware image file: hdc-0.11-new.img, please download it from http://www.oldlinux.org, after downloading it, or cd tools;tar -xvf hdc-0.11-new.img.

and you'd better install tools/calltree, tools/tree2dotx yourself: just copy
them to /usr/bin, of course, you'd compile calltree at first.

# 2. hack linux-0.11

get help from the main Makefile of linux-0.11 and star to hack it.

$ cd linux-0.11
$ make help		// get help
$ make  		// compile
$ make start		// boot it on qemu
$ make debug		// debug it via qemu & gdb, you'd start gdb to connect it.
$ make tags		// create the tag file from the source code
$ make cscope		// create the cscope index database from the source code

NOTE!

there is a calltree in tools/, which can help you to analyze the source code
via printing the calling tree of some indicated functions.

compile
$ cd tools/calltree-2.3
install
$ sudo cp ./calltree/OBJ/i686-linux-cc/calltree /usr/bin
use
$ calltree 		// just type calltree and get the help

# 3. debug

start the kernel with qemu, which will listening on port 1234

$ cd linux-0.11
$ make debug		

open a new terminal, start gdb and connect the gdbstub in qemu

$ gdb linux-0.11/tools/system
(gdb) break main
(gdb) target remote localhost:1234
(gdb) s			// si:assembly instruction, s|n: c statement(s will enter into subfunc)
(gdb) ...

# 4. Known issues
	1. The shell command line will give you some Not owner
		eg:
			cp hello.c test.c
			cp: test.c: Not owner

References & Links

[1] https://github.com/yuanxinyu/Linux-0.11
[2] https://github.com/run/linux0.11
