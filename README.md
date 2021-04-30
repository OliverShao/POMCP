# POMCP

## INSTALLATION

1. ```cd``` to the directory containing the package's source code and type
     ```./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu``` to configure the package for your system.

     Running ```configure``` might take a while.  While running, it prints
     some messages telling which features it is checking for.

  2. Type ```make``` to compile the package.

  3. Optionally, type ```make check``` to run any self-tests that come with
     the package.

  4. Type ```make install``` to install the programs and any data files and
     documentation.

  5. You can remove the program binaries and object files from the
     source code directory by typing ```make clean```.  To also remove the
     files that ```configure``` created (so you can compile the package for
     a different kind of computer), type ```make distclean```.  There is
     also a ```make maintainer-clean``` target, but that is intended mainly
     for the package's developers.  If you use it, you may have to get
     all sorts of other programs in order to regenerate files that came
     with the distribution.

Details are in Author's steps in [INSTALL](https://github.com/OliverShao/POMCP/blob/main/INSTALL). Note: use ```./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu``` instead of ```./configure``` to solve ```configure: error: Could not link against !```

## RUN

### Compile
```make``` to compile

### Run RockSample game
Under /src, for example, run ```./pomcp --problem rocksample --size 11 --number 11 --timeout 10000 --maxdouble 15 --rolloutknowledge 2 --outputfile ro_s11_n11_GeneratePreferred.txt``` This will simulate the game on a 11x11 board with 11 rocks, and the result will be stored in the 'outputfile'.

--rolloutknowledge == 4 is running on multiple policies using Switch-Case.
--rolloutknowledge == 2 is running on ONE policy.(By Default, it runs GeneratePreferred() ).
