OFILES= bins.o
OFILES1= bSort.o misc.o
CPATH=/usr/lib/llvm-3.4/bin/
LLVMASY=$(CPATH)llvm-as
LLVMOPT=$(CPATH)opt
LLVMLC=$(CPATH)llc
AS=clang
LD=ld
CC=clang++
C=clang
LD=clang++
CXXFLAGS=`$(CPATH)llvm-config --cppflags`
LDFLAGS=`$(CPATH)llvm-config --ldflags --libs core jit native`

LIBS=

all: bins bSort

bins: $(OFILES)
	$(LD) $(OFILES) $(LIBS) -o $@

bSort: $(OFILES1)
	$(LD) $(OFILES1) $(LIBS) -o $@


%.o : %.s
	$(AS) -c $< -o $@

%.s : %.bc
	$(LLVMLC) $< -o $@

%.bc : %.llvm
	$(LLVMASY) $< -o $@

%.o %.d : %.C
	$(CC) -g -c -x c++ $(CXXFLAGS) $< -MD 

%.o %.d : %.c
	$(C) -g -c $(CXXFLAGS) $< -MD

clean:
	rm -rf *.o *.s *.bc bins bSort *~
