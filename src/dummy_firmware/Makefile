
ARMGNU = arm-none-eabi

AOPS = --warn --fatal-warnings -mcpu=cortex-m4
COPS = -Wall -Werror -O2 -nostdlib -nostartfiles -ffreestanding  -mcpu=cortex-m4 -mthumb \
       -I$(PWD)/libmspprintf/src/include

IRQS = 163,164:mbox_have_data_isr

OBJS = \
       vectors.o \
       trch.o \
       isr.o \
       command.o \
       mailbox.o \
       nvic.o \
       reset.o \
       libmspprintf/src/printf.o \
       uart.o \

all : trch.elf

clean:
	rm -f *.o
	rm -f *.elf
	rm -f *.list
	rm -f vectors.s isr.c

vectors.s isr.c: genisr.py
	./genisr.py --handlers $(IRQS) vectors.s isr.c

%.o : %.s
	$(ARMGNU)-as $(AOPS) $< -o $@

%.o : %.c
	$(ARMGNU)-gcc $(COPS) -c $< -o $@

trch.elf: trch.ld $(OBJS)
	$(ARMGNU)-ld -o $@ -T $^
