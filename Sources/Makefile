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
	@if ! [ -d ./bin/ ] ; then mkdir -p ./bin ; fi
	@echo "[LD] $(KERNEL)"
	@$(LD) $(LDFLAGS) $(OBJECTS) -o $(KERNEL)

%.o: %.asm
	@echo "[AS] $@"
	@$(AS) $(ASFLAGS) $< -o $@

%.o: %.c
	@echo "[CC] $@"
	@$(CC) $(CFLAGS) $< -o $@

clean:
	@echo "Cleaning compiled objects..."
	@rm -vRf $(OBJECTS) $(KERNEL) ./bin

run: $(KERNEL)
	@echo "Running kernel test..."
	@$(QEMU) -m 32 -monitor stdio -kernel $(KERNEL)
