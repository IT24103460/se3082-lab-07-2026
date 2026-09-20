# Exercise 8: build and run all 6 programs from their exercise folders.
# Run from inside Exercise08:  make  /  make run  /  make timings  /  make clean

CC     = mpicc
CFLAGS = -O2 -Wall
NP    ?= 4
# Add --oversubscribe if you run with more processes than CPU cores
MPIRUN_FLAGS ?=

PROGS = ex1 ex2 ex3 ex4 ex5 ex6

.PHONY: all run timings clean

all: $(PROGS)

ex1: ../Exercise01/ex1.c
	$(CC) $(CFLAGS) -o $@ $<
ex2: ../Exercise02/ex2.c
	$(CC) $(CFLAGS) -o $@ $<
ex3: ../Exercise03/ex3.c
	$(CC) $(CFLAGS) -o $@ $<
ex4: ../Exercise04/ex4.c
	$(CC) $(CFLAGS) -o $@ $<
ex5: ../Exercise05/ex5.c
	$(CC) $(CFLAGS) -o $@ $<
ex6: ../Exercise06/ex6.c
	$(CC) $(CFLAGS) -o $@ $<

# Run every program with NP processes (default 4)
run: all
	@for p in $(PROGS); do \
		echo "=================== $$p (np=$(NP)) ==================="; \
		mpirun $(MPIRUN_FLAGS) -np $(NP) ./$$p; \
		echo; \
	done

# Exercise 7 helper: timing lines only, for 2, 4 and 8 processes
timings: all
	@for np in 2 4 8; do \
		echo "---- np = $$np ----"; \
		for p in $(PROGS); do \
			mpirun $(MPIRUN_FLAGS) -np $$np ./$$p | grep "Time"; \
		done; \
	done

clean:
	rm -f $(PROGS)