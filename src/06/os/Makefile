PREFIX  = /usr
ARCH    = h8300-hms
BINDIR  = $(PREFIX)/bin
ADDNAME = $(ARCH)-

AR      = $(BINDIR)/$(ADDNAME)ar
AS      = $(BINDIR)/$(ADDNAME)as
CC      = $(BINDIR)/$(ADDNAME)gcc
LD      = $(BINDIR)/$(ADDNAME)ld
NM      = $(BINDIR)/$(ADDNAME)nm
OBJCOPY = $(BINDIR)/$(ADDNAME)objcopy
OBJDUMP = $(BINDIR)/$(ADDNAME)objdump
RANLIB  = $(BINDIR)/$(ADDNAME)ranlib
STRIP   = $(BINDIR)/$(ADDNAME)strip

OBJCHG  = ../../tools/objchg/objchg
OBJS    = startup.o main.o
OBJS   += lib.o serial.o

TARGET  = kozos

CFLAGS  = -Wall -mh -nostdinc -nostdlib -fno-builtin
#CFLAGS += -mint32      # intを32ビットにすると掛算/割算ができなくなる
CFLAGS += -I.
#CFLAGS += -g
CFLAGS += -Os #-Wno-pointer-sign
CFLAGS += -DKOZOS

LFLAGS = -static -T ld.scr -L.

.SUFFIXES:	.c .o
.SUFFIXEs:	.s .o

all:		$(TARGET)

$(TARGET):	$(OBJS)
		$(CC) $(OBJS) -o $(TARGET) $(CFLAGS) $(LFLAGS)
		mv $(TARGET).exe $(TARGET)
		cp $(TARGET) $(TARGET).coff
		$(STRIP) $(TARGET)
		$(OBJCHG) -f coff -t elf -i $(TARGET) -o $(TARGET).elf
		cp $(TARGET).elf $(TARGET)

.c.o:		$<
		$(CC) -c $(CFLAGS) $<

.s.o:		$<
		$(CC) -c $(CFLAGS) $<

clean:
		rm -f $(OBJS) $(TARGET) $(TARGET).coff $(TARGET).elf
