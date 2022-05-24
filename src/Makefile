CC=gcc
OPTS=-g -std=c99 -Werror

all: main.o cache.o
	$(CC) $(OPTS) -O3 -o cache main.o cache.o -lm

main.o: main.c cache.h
	$(CC) $(OPTS) -O3 -c main.c

cache.o: cache.h cache.c
	$(CC) $(OPTS) -O3 -c cache.c

clean:
	rm -f *.o cache;
