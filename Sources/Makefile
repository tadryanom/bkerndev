AS = nasm
CC = gcc
LD = ld
QEMU = qemu-system-i386
ASFLAGS = -f elf
CFLAGS = -m32 -Wall -Wextra -Werror -O -nostdlib -nostdinc -fno-builtin \
	-nostartfiles -nodefaultlibs -fno-stack-protector -fstrength-reduce \
	-fomit-frame-pointer -finline-functions -I./include -c
LDFLAGS = -T ./script/link.ld -melf_i386
OBJECTS = ./boot/start.o ./kernel/main.o ./kernel/scrn.o ./kernel/gdt.o \
	./kernel/idt.o ./kernel/isrs.o ./kernel/irq.o ./kernel/timer.o \
	./kernel/kb.o

all: ./bin/kernel.elf

./bin/kernel.elf: $(OBJECTS)
	$(LD) $(LDFLAGS) $(OBJECTS) -o ./bin/kernel.elf

%.o: %.asm
	$(AS) $(ASFLAGS) $< -o $@

%.o: %.c
	$(CC) $(CFLAGS) $< -o $@

clean:
	rm -vrf ./boot/*.o ./kernel/*.o ./bin/kernel.elf

run: ./bin/kernel.elf
	$(QEMU) -m 32 -monitor stdio -kernel ./bin/kernel.elf
