OBJECTS = start.o main.o scrn.o gdt.o idt.o isrs.o irq.o timer.o util.o kb.o
CC = gcc
CFLAGS = -m32 -Wall -Wextra -Werror -O -fno-pie -fno-stack-protector \
	-nostartfiles -nodefaultlibs -nostdlib -fstrength-reduce \
	-fomit-frame-pointer -finline-functions -nostdinc -fno-builtin \
	-I./include -c
LD = ld
LDFLAGS = -melf_i386 -T link.ld
AS = nasm
ASFLAGS = -f elf

all: kernel.elf

kernel.elf: $(OBJECTS)
	$(LD) $(LDFLAGS) $(OBJECTS) -o $@

%.o: %.c
	$(CC) $(CFLAGS)  $< -o $@

%.o: %.asm
	$(AS) $(ASFLAGS) $< -o $@

clean:
	rm -vrf *.o kernel.elf
