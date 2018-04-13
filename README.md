# c-boilerplate
A Boilerplate For C Application with Googletest and Code Analyzer Support

### Preliminary
This boilerplate provides an easy-to-use generic C makefile for starting C application development in Linux environment. In addition to basic compile functionalities, the makefile also takes Googletest and code analyzers into account.

Specifically, this boilerplate would be a good starting point if you wish to start trying out [Test-Driven Development (TDD)](https://en.wikipedia.org/wiki/Test-driven_development) or develop your code under the [Google discipline](https://google.github.io/styleguide/cppguide.html).

### Compiler Settings

| Variable   | Description                                    | Default       |
|------------|------------------------------------------------|---------------|
| `BINARY`   | Name of the binary you wish to output          | `app`         |
| `CROSS`    | Cross-compiler prefix                          |               |
| `CC`       | GNU compiler command                           | `$(CROSS)gcc` |
| `STD`      | GCC compile standard option                    | `-std=gnu99`  |
| `CPPFLAGS` | Common flags for C preprocessor (`-I` options) | `-I.`         |
| `LDFLAGS`  | Common library locations (`-L` options)        |               |
| `LDLIBS`   | Common libraries to be loaded (`-l` options)   |               |

Many of the options are actually GNU make implicit variables. We just overwrite or extend the default values, so that you can easily integrate the makefile to your building environment.

You can also use target-specific variable values to update the compiler setting for each target.

### Compile your codes
If you have any written source codes, put them inside the `src` folder.

If you have any written unit tests, put them inside the `unittest` folder, in the same level as the `src` folder.

#### Creating release build
```
make
```

#### Creating debug build
```
make debug
```

#### Creating shared library
```
make shlib
```

#### Creating Googletest binary
```
make gtest
```

### Utilities
Some utility commands are shipped with the generic makefile.

#### Clean-up intermediate files and binary
```
make clean
```

#### Call static code analyzer to check your source code (via [cppcheck](http://cppcheck.sourceforge.net))
```
make cppcheck
```

#### Call linter to lint your source code (via [cpplint](https://github.com/cpplint/cpplint))
```
make cpplint
```

#### Execute the binary
```
make run
```

#### Beautify your source code (via [astyle](http://astyle.sourceforge.net))
```
make style
```

#### Call dynamic code analyzer to check your binary (via [valgrind](http://valgrind.org))
```
make valgrind
```

### License
This boilerplate is distributed with MIT License.
