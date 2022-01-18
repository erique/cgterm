# Makefile for AmigaOS 4.0

DESTDIR=x-`date lformat %m%d.%H%M%`
PREFIX=
CC=gcc

# for clib2:
CFLAGS=-D__USE_NETINET_IN_H -D__USE_INLINE__ -D__amiga_clib2__ -O3 -Wall -ISDK:Local/clib2/include/SDL -DPREFIX=\"$(PREFIX)\"
LDFLAGS=-lunix -lSDL -lnet -lauto -lm

# for newlib:
#CFLAGS=-newlib -O3 -Wall -ISDK:Local/newlib/include/SDL -DPREFIX=\"$(PREFIX)\"
#LDFLAGS=-newlib -LSDK:Local/newlib/lib -lSDL -lauto -lm


OBJS= \
	kernal.o \
	gfx.o \
	net.o \
	config.o \
	keyboard.o \
	menu.o \
	font.o \
	timer.o \
	crc.o \
	sound.o \
	macro.o \
	ui.o

TERMOBJS= \
	xfer.o \
	xmodem.o \
	punter.o \
	diskimage.o \
	dir.o \
	fileselector.o \
	ui_term.o

CHATOBJS= \
	chat.o \
	status.o \
	ui_chat.o

EDITOBJS= \
	ui_edit.o \
	fileselector.o \
	dir.o \
	diskimage.o


%.o: %c
	$(CC) $(CFLAGS) -c $<


.PHONY: install installdirs clean


all: cgterm cgchat cgedit testkbd

cgterm: cgterm.o $(OBJS) $(TERMOBJS)
	$(CC) -o cgterm $^ $(LDFLAGS)

cgchat: cgchat.o $(OBJS) $(CHATOBJS)
	$(CC) -o cgchat $^ $(LDFLAGS)

cgedit: cgedit.o $(OBJS) $(EDITOBJS)
	$(CC) -o cgedit $^ $(LDFLAGS)

testkbd: testkbd.o
	$(CC) -o testkbd $^ $(LDFLAGS)

testimage: testimage.c diskimage.c dir.c
	$(CC) -g -O3 -Wall -o testimage $^

install: all installdirs
	strip cgterm
	strip cgchat
	strip cgedit
	strip testkbd
	copy cgterm $(DESTDIR)/CGTerm
	copy cgchat $(DESTDIR)/CGChat
	copy cgedit $(DESTDIR)/CGEdit
	copy testkbd $(DESTDIR)/TestKeyboard
	copy *.info *.bmp *.kbd *.wav $(DESTDIR)/data

installdirs: 
	makedir $(DESTDIR)/data all

clean:
	delete cgterm cgchat cgedit testkbd *.o
