PROJECT           := app
LIBRARY           := lib$(PROJECT).so

## -- Compiler Settings
CROSS             ?=
CC                := $(CROSS)gcc
STD               := -std=gnu99

override CPPFLAGS += -I.
override CFLAGS   += $(STD) -O3 -Wall -Werror -Wextra -MP -MMD
override CFLAGS   += -D_GNU_SOURCE
override LDFLAGS  += -L.
override LDLIBS   +=

EXCLUDE           := -path ./example -prune -o
SOURCES           := $(shell find . $(EXCLUDE) -name "*.c" -print)
OBJECTS            = $(addsuffix .o,$(basename $(SOURCES)))
DEPENDS            = $(addsuffix .d,$(basename $(OBJECTS)))


## -- Compilation
.PHONY: all debug lib test
.DELETE_ON_ERROR:

all: CFLAGS       += -DNDEBUG
all: $(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) $(OBJECTS) -o $(PROJECT)

debug: CFLAGS     += -g
debug: $(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) $(OBJECTS) -o $(PROJECT)

lib: CFLAGS       += -fPIC -DNDEBUG
lib: LDLIBS       += -lc
lib: $(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) -shared $(OBJECTS) -o $(LIBRARY)

test: CC          := $(CROSS)g++
test: CXX         := $(CROSS)g++
test: STD         := -std=c++98
test: CFLAGS      += -DUNITTEST
test: CXXFLAGS     = $(CFLAGS)
test: LDLIBS      += -lgtest -lgtest_main
test: SOURCES     := $(shell find . $(EXCLUDE) -name "*.c*" -print)
.SECONDEXPANSION:
test: $$(OBJECTS)
	$(CC) $(LDFLAGS) $(LDLIBS) $(OBJECTS) -o $(PROJECT)

-include $(DEPENDS)


.PHONY: clean run
.ONESHELL:

clean:
	@find . -type f -executable | xargs $(RM)
	@find . -name "*.[ado]" | xargs $(RM)

run:
	@find . -type f -executable ! -name "*.so" | xargs sh -c


.PHONY: cppcheck cpplint style valgrind
.ONESHELL:

cppcheck:
	@cppcheck --enable=all --std=c99 --std=posix \
		--suppress=missingIncludeSystem \
		-f .

cpplint:
	@cpplint --linelength=80 --recursive \
		--filter=-legal/copyright,-build/header_guard \
		.

style:
	@astyle -Qnrv --style=google --indent=spaces=4 --lineend=linux \
		--convert-tabs --indent-switches \
		"*.c" "*.h"

valgrind: clean debug
	@valgrind --leak-check=full --show-leak-kinds=all ./$(PROJECT)
