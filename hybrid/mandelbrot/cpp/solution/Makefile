ifeq ($(COMP),)
COMP=intel
endif

COMMONDIR=../../../heat-equation/common

ifeq ($(COMP),intel)
CXX=icpc
CC=icc
CCFLAGS=-g -qopenmp -O3 -xHost -I$(COMMONDIR)
LDFLAGS=
LIBS=-lpng
endif

ifeq ($(COMP),gnu)
FC=gfortran
CC=gcc
FCFLAGS=-fopenmp -O3 -Wall
CCFLAGS=-fopenmp -O3 -Wall -I$(COMMONDIR)
LDFLAGS=
LIBS=-lpng
endif

ifeq ($(COMP),cray)
FC=ftn
CC=cc
CXX=CC
FCFLAGS=-fopenmp -O3
CCFLAGS=-fopenmp -I$(COMMONDIR) -O3
LDFLAGS=
LIBS=-lpng
endif

EXE=mandelbrot
OBJS=mandelbrot.o
OBJS_PNG=pngwriter.o
CORRECT_OBJS_PNG=$(COMMONDIR)/pngwriter.o

all: $(EXE)

$(COMMONDIR)/pngwriter.o: $(COMMONDIR)/pngwriter.c $(COMMONDIR)/pngwriter.h
mandelbrot.o: mandelbrot.cpp

pngwriter.o: pngwriter.c pngwriter.h
	$(CC) $(CCFLAGS) -c -o $@ $<

$(EXE): $(OBJS) $(OBJS_PNG)
	$(CC) $(CCFLAGS) $(OBJS) $(OBJS_PNG) -o $@ $(LDFLAGS) $(LIBS)

%.o: %.F90
	$(FC) $(FCFLAGS) -c $< -o $@

%.o: %.cpp
	$(CXX) $(CCFLAGS) -c $< -o $@

%.o: %.c
	$(CC) $(CCFLAGS) -c $< -o $@

.PHONY: clean
clean:
	-/bin/rm -f $(EXE) a.out *.o *.mod *.png *~ mandelbrot.png
