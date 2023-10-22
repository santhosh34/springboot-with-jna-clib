Steps to make a shared library from this repo: 

1) Run the following commands: 
    cd springboot-with-jna-clib/sharedlib/src/calc
    gcc -shared -fPIC -o libmaths.dylib mul.c add.c

2) gcc -L$(PWD) -WL,-R$(PWD) -o main main.c -lcalc 
    gcc -L<<springboot-with-jna-clib>>path/sharedlib/src/calc  -o main main.c -lcalc 
    
    export DYLD_LIBRARY_PATH=$DYLD_LIBRARY_PATH:<<springboot-with-jna-clib>>path/sharedlib/src/calc
    ./main 
        -L <dir>Add directory to library search path
        -o <file>               Write output to <file>
        -l specific library name. 
        -WL   Pass the comma separated arguments in <arg> to the linker
        
        Type: gcc -help in mac to get the following help notes

         -Wl,<arg>               Pass the comma separated arguments in <arg> to the linker
         -l namespec OR --library=namespec
            Add the archive or object file specified by namespec to the list of files to link. This option may be used any number of times. If namespec is of the form :filename, ld will search the library path for a file called filename, otherwise it will search the library path for a file called *lib*namespec.a.

            On systems which support shared libraries, ld may also search for files other than libnamespec.a. Specifically, on ELF and SunOS systems, ld will search a directory for a library called libnamespec.so before searching for one called libnamespec.a. (By convention, a .so extension indicates a shared library.) Note that this behavior does not apply to :filename, which always specifies a file called filename.

            The linker will search an archive only once, at the location where it is specified on the command line. If the archive defines a symbol which was undefined in some object which appeared before the archive on the command line, the linker will include the appropriate file(s) from the archive. However, an undefined symbol in an object appearing later on the command line will not cause the linker to search the archive again.

       
