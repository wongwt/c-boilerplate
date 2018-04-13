BINARY            := app

## -- Compiler Settings
CROSS             ?=
CC                := $(CROSS)gcc
STD               := -std=gnu99

override CPPFLAGS += -I.
override CFLAGS   += $(STD) -O3 -Wall -Werror -Wextra -MP -MMD -D_GNU_SOURCE
override LDFLAGS  +=
override LDLIBS   +=

SOURCES           := $(shell find . -name "*.c")
OBJECTS            = $(addsuffix .o,$(basename $(SOURCES)))
DEPENDS            = $(addsuffix .d,$(basename $(OBJECTS)))


## -- Compilation
.PHONY: all debug gtest shlib
.DELETE_ON_ERROR:

all: CFLAGS       += -DNDEBUG
all: $(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) $(OBJECTS) -o $(BINARY)

debug: CFLAGS     += -g
debug: $(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) $(OBJECTS) -o $(BINARY)_debug

gtest: CC         := $(CROSS)g++
gtest: CXX        := $(CROSS)g++
gtest: STD        := -std=c++98
gtest: CFLAGS     += -DUNITTEST
gtest: CXXFLAGS    = $(CFLAGS)
gtest: LDLIBS     += -lgtest -lgtest_main
gtest: SOURCES    := $(shell find .. -name "*.c" -or -name "*.cpp")
.SECONDEXPANSION:
gtest: $$(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) $(OBJECTS) -o $(BINARY)_gtest

shlib: CFLAGS     += -fPIC
shlib: $(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) -shared $(OBJECST) -o lib$(BINARY).so

-include $(DEPENDS)


## -- Utilities
.PHONY: clean cppcheck cpplint run style valgrind
.ONESHELL:

clean:
	@find .. -executable -type f | xargs $(RM)
	@find .. -name "*.[ado]" | xargs $(RM)

cppcheck:
	@cppcheck --enable=all --std=c99 --std=posix \
		--suppress=missingIncludeSystem \
		-f .

cpplint:
	@cpplint --linelength=80 --recursive \
		--filter=-legal/copyright,-build/header_guard \
		.

run:
	@find . -executable -type f -not -name "*.so" | xargs sh -c

style:
	@astyle -Qnrv --style=google --indent=spaces=4 --lineend=linux \
		--convert-tabs --indent-switches \
		"*.c" "*.h"

valgrind: clean debug
	@valgrind --leak-check=full --show-leak-kinds=all \
		./$(BINARY)_debug
