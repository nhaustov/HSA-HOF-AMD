## Copyright 2014 HSA Foundation Inc.  All Rights Reserved.
##
## HSAF is granting you permission to use this software and documentation (if
## any) (collectively, the "Materials") pursuant to the terms and conditions
## of the Software License Agreement included with the Materials.  If you do
## not have a copy of the Software License Agreement, contact the  HSA Foundation for a copy.
## Redistribution and use in source and binary forms, with or without
## modification, are permitted provided that the following conditions
## are met:
## 1. Redistributions of source code must retain the above copyright
##    notice, this list of conditions and the following disclaimer.
## 2. Redistributions in binary form must reproduce the above copyright
##    notice, this list of conditions and the following disclaimer in the
##    documentation and/or other materials provided with the distribution
## THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
## IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
## FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
## CONTRIBUTORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
## LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
## FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS WITH THE SOFTWARE.

HSA_INCLUDE = /opt/hsa/include
HSA_LIB = /opt/hsa/lib

LFLAGS= -Wl,--unresolved-symbols=ignore-in-shared-libs 

CXX := g++

CPP_FILES := $(wildcard *.cpp)

OBJ_FILES := $(notdir $(CPP_FILES:.cpp=.o))

HSAIL_FILES = globals.hsail
FINALIZED_OBJ = globals.o

all: hof_example $(FINALIZED_OBJ)

hof_example: $(OBJ_FILES)
	$(CXX) $(LFLAGS) $(OBJ_FILES) -L$(HSA_LIB) -lhsa-runtime64 -lhsa-runtime-ext64 -o hof_example

%.o: %.cpp
	$(CXX) -c -I$(HSA_INCLUDE) -o $@ $< -std=c++11

$(FINALIZED_OBJ): $(HSAIL_FILES)
	../bin/hof -output=$(FINALIZED_OBJ) -hsail $(HSAIL_FILES)

clean:
	rm -rf *.o hof_example
