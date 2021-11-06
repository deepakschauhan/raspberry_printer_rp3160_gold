CC=gcc
RM=rm -f
CFLAGS=-Wl,-rpath,/usr/lib -Wall -fPIC -O3 -std=gnu89
LDFLAGS=
LDLIBS=-lcupsimage -lcups

SRCS=rastertorp3160.c
OBJS=$(subst .c,.o,$(SRCS))

all: rastertorp3160

rastertorp3160: $(OBJS)
	gcc $(LDFLAGS) -o rastertorp3160 rastertorp3160.o $(LDLIBS)

rastertorp3160.o: rastertorp3160.c
	gcc $(CFLAGS) -c rastertorp3160.c

clean:
	rm -f rastertorp3160 rastertorp3160.o
