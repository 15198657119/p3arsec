# Makefile for parallel simulated annealer

PREFIX=${PARSECDIR}/pkgs/kernels/canneal/inst/${PARSECPLAT}

TARGET=canneal
LIBS:=$(LIBS) -lm
THREADFILE:=annealer_thread.cpp

ifdef version
  ifeq "$(version)" "pthreads"
    CXXFLAGS+=-DENABLE_THREADS -pthread
  endif
  ifeq "$(version)" "ff"
    CXXFLAGS+=-DENABLE_THREADS -DENABLE_FF -pthread
    THREADFILE:=annealer_thread_ff.cpp
  endif
  ifeq "$(version)" "nornir"
    CXXFLAGS+=-DENABLE_THREADS -DENABLE_NORNIR_NATIVE -pthread
    THREADFILE:=annealer_thread_nornir.cpp
  endif
endif

all:
	$(CXX) $(CXXFLAGS) $(THREADFILE) -c -o annealer_thread.o
	$(CXX) $(CXXFLAGS) rng.cpp -c -o rng.o
	$(CXX) $(CXXFLAGS) netlist.cpp -c -o netlist.o
	$(CXX) $(CXXFLAGS) main.cpp -c -o main.o
	$(CXX) $(CXXFLAGS) netlist_elem.cpp -c -o netlist_elem.o
	$(CXX) $(CXXFLAGS) $(LDFLAGS) *.o $(LIBS) -o $(TARGET)

clean:
	rm -f *.o $(TARGET)

install:
	mkdir -p $(PREFIX)/bin
	cp -f $(TARGET) $(PREFIX)/bin/$(TARGET)

