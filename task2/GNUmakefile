RSYNC = rsync
SSH = ssh

SFLAGS = -F '../.ssh-cfg'
RFLAGS = --recursive --progress --copy-links --exclude=build/ -e "$(SSH) $(SFLAGS)"

HOST = saturn
REMOTEDIR = ~/advanced_multiprocessor_programming/task2
REMOTEPHEETDIR = ~
SOURCE = . ../CMakeModules
PHEETDIR = ../../pheet
AMPDIR = ../advanced_multiprocessor_programming/task2/build/src/

all: check

bake:
	mkdir -p build
	cd build; cmake -DCMAKE_BUILD_TYPE="Debug" ..; make -j6
	
check: bake
	cd build; ctest --output-on-failure

bench: bake
	cd $(PHEETDIR) && make test && LD_LIBRARY_PATH=$(AMPDIR) bin/pheet_test

hand-in:
	$(RSYNC) $(RFLAGS) $(PHEETDIR) $(HOST):$(REMOTEPHEETDIR)
	$(RSYNC) $(RFLAGS) $(SOURCE) $(HOST):$(REMOTEDIR)

clean:
	rm -rf build
