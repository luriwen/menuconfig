CFLAGS  := -I/usr/include/ncurses -DCURSES_LOC="<ncurses.h>" -DLOCALE -Wall -Wmissing-prototypes -Wstrict-prototypes -O2 -fomit-frame-pointer
LDFLAGS := -lncurses

cc := gcc

all : prepare lxdialog mconf conf

%.o : %.c
	gcc -c $(CFLAGS) $(LDFLAGS) $< -o $@

prepare :
	cp zconf.hash.c_shipped zconf.hash.c
	cp zconf.lex.c_shipped zconf.lex.c
	cp zconf.tab.c_shipped zconf.tab.c

zconf.tab.o : zconf.hash.c zconf.lex.c zconf.tab.c

lxdialog := lxdialog/checklist.o lxdialog/util.o lxdialog/inputbox.o
lxdialog +=	lxdialog/textbox.o lxdialog/yesno.o lxdialog/menubox.o

qconf : zconf.tab.o
	gcc -o $@ $^ $(LDFLAGS)

mconf : mconf.o zconf.tab.o $(lxdialog)
	gcc -o $@ $^ $(LDFLAGS)

conf : conf.o zconf.tab.o $(lxdialog)
	gcc -o $@ $^ $(LDFLAGS)

clean :
	find -name "*.o" -exec rm "{}" \;
	-rm conf mconf zconf.*.c
