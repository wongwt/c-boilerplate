# c-boilerplate
A Boilerplate For C Application with Googletest and Code Analyzer Support

### Preliminary
This boilerplate provides an easy-to-use generic C makefile for starting C application development in Linux environment. In addition to basic compile functionalities, the makefile also takes Googletest and code analyzers into account.

Specifically, this boilerplate would be a good starting point if you wish to start trying out [Test-Driven Development (TDD)](https://en.wikipedia.org/wiki/Test-driven_development) or develop your code under the [Google discipline](https://google.github.io/styleguide/cppguide.html).

### Compiler Settings

| Variable   | Description                                    | Default                     |
|------------|------------------------------------------------|-----------------------------|
| `PROJECT`  | Project name                                   | `app`                       |
| `DESTDIR`  | Destination directory                          |                             |
| `PREFIX`   | Installation directory prefix                  | `/usr`                      |
| `CROSS`    | Cross-compiler prefix                          |                             |
| `CC`       | GNU compiler command                           | `$(CROSS)gcc`               |
| `STD`      | GCC compile standard option                    | `-std=gnu99`                |
| `CPPFLAGS` | Common flags for C preprocessor (`-I` options) | `-I.`                       |
| `LDFLAGS`  | Common library locations (`-L` options)        | `-L.`                       |
| `LDLIBS`   | Common libraries to be loaded (`-l` options)   |                             |
| `EXCLUDE`  | Directory to exclude in source searching       |                             |

Many of the options are actually GNU make implicit variables. We just overwrite or extend the default values, so that you can easily integrate the makefile to your building environment.

You can also use target-specific variable values to update the compiler setting for each target.

### Compile your codes
If you have any written source codes, put them inside the `src` folder.

If you have any written unit tests, put them inside the `unittest` folder, under the `src` folder.

| Command      | Description                                    |
|--------------|------------------------------------------------|
| `make`       | Create release build                           |
| `make debug` | Create debug build                             |
| `make lib`   | Creare shared library                          |
| `make test`  | Create Googletest binary                       |

### Utilities
Some utility commands are shipped with the generic makefile.

#### Handling compiled binary
| Command         | Description                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------|
| `make clean`    | Clean-up intermediate files and binary                                                                |
| `make distclean`| Remove project binary/library from specified location and clean-up intermediate files and binary      |
| `make install`  | Install project binary/library to specified location                                                  |
| `make run`      | Execute the binary                                                                                    |
| `make uninstall`| Remove project binary/library from specified location                                                 |

#### Source code analyze
| Command         | Description                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------|
| `make cppcheck` | Call static code analyzer to check your source code (via [cppcheck](http://cppcheck.sourceforge.net)) |
| `make cpplint`  | Call linter to lint your source code (via [cpplint](https://github.com/cpplint/cpplint))              |
| `make style`    | Beautify your source code (via [astyle](http://astyle.sourceforge.net))                               |
| `make valgrind` | Call dynamic code analyzer to check your binary (via [valgrind](http://valgrind.org))                 |

### License
This boilerplate is distributed with MIT License.
