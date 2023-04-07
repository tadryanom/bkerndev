## Tools
AS = nasm
CC = gcc
LD = ld
QEMU = qemu-system-i386

## Assembler and compiller flags
ASFLAGS = -f elf
CFLAGS = -m32 -Wall -Wextra -Werror -O -nostdlib -nostdinc -fno-builtin \
	-nostartfiles -nodefaultlibs -fno-stack-protector -fstrength-reduce \
	-fomit-frame-pointer -finline-functions -I./include -c
LDFLAGS = -T ./script/link.ld -melf_i386

## Files to assembly, to compile and to link
OBJECTS = ./boot/start.o ./kernel/main.o ./kernel/scrn.o ./kernel/gdt.o \
	./kernel/idt.o ./kernel/isrs.o ./kernel/irq.o ./kernel/timer.o \
	./kernel/kb.o
KERNEL = ./bin/kernel.elf

## Here do it: assembly, compile, link, clean and run
all: $(KERNEL)

$(KERNEL): $(OBJECTS)
	@if ! [ -d ./bin/ ] ; then mkdir -vp ./bin ; fi
	$(LD) $(LDFLAGS) $(OBJECTS) -o $(KERNEL)

%.o: %.asm
	$(AS) $(ASFLAGS) $< -o $@

%.o: %.c
	$(CC) $(CFLAGS) $< -o $@

clean:
	rm -vf ./boot/*.o ./kernel/*.o $(KERNEL)

run: $(KERNEL)
	$(QEMU) -m 32 -monitor stdio -kernel $(KERNEL)
