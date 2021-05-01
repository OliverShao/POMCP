# POMCP

This code is an application of [Monte-Carlo Planning in Large POMDPs](https://papers.nips.cc/paper/2010/file/edfbe1afcf9246bb0d40eb4d8027d90f-Paper.pdf).

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

Details are in Original Authors' steps in [INSTALL](https://github.com/OliverShao/POMCP/blob/main/INSTALL). Note: use ```./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu``` instead of ```./configure``` to solve ```configure: error: Could not link against !```

## RUN

### Compile
```make``` to compile.

### Run RockSample game
Under /src, for example, run ```./pomcp --problem rocksample --size 11 --number 11 --timeout 10000 --maxdouble 15 --rolloutknowledge 2 --outputfile ro_s11_n11_GeneratePreferred.txt``` This will simulate the game on a 11x11 board with 11 rocks, and the result will be stored in the 'outputfile'.

--rolloutknowledge == 4 is running on multiple policies using Switch-Case.
--rolloutknowledge == 2 is running on ONE policy.(By Default, it runs GeneratePreferred() ).

## CHANGES MADE

### RockSample Problem
My new code is particularly written for "rocksample" problem, which is one of the problems provided by the orginal authors [David Silver](https://www.davidsilver.uk/) and Joel Veness. The RockSample problem(game) is originally developed to test heuristic search value iteration(HSVI) in this [paper](https://arxiv.org/pdf/1207.4166.pdf). Other games are Battleship and Pocman.

### Existing Effort
The original SelectRandom() function in [simulator.cpp](https://github.com/OliverShao/POMCP/blob/main/src/simulator.cpp) has 3 rolloutlevels: 0-pure randomly select one action(may be illegal); 1-randomly select one action from a vector of actions return by GenerateLegal() function in derived class in [rocksample.cpp](https://github.com/OliverShao/POMCP/blob/main/src/rocksample.cpp), which only contains legal actions; 2-randomly select a "preferred" action from a vector of actions return by GeneratePreferred() in derived class in [rocksample.cpp](https://github.com/OliverShao/POMCP/blob/main/src/rocksample.cpp), which filters actions based on observations. There are three types of actions: Sample, Move(north, south, east, west), Observe(rock0, rock1,...,rockN-1).

### New Changes
A new rollout level is added in SelectRandom() function in [simulator.cpp](https://github.com/OliverShao/POMCP/blob/main/src/simulator.cpp): 3-Multi-Policies, where the simulator switches among policies. 

Besides, two new policies are added in [rocksample.cpp](https://github.com/OliverShao/POMCP/blob/main/src/rocksample.cpp): Generate_GoToMostPreferred and GenerateSimplePolicy_GoToNearestRock. The Generate_GoToMostPreferred is modified based on GeneratePreferred policy. It would only push the MOVE action that go to the most possible valuable rock based on previous observations. The GenerateSimplePolicy_GoToNearestRock is design to move the agent towards or observe on the nearest rock. This idea is based on the fact that the correctness of observation on a rock is better when the rock is closer.

A visualization python notebook [plot_evaluation_data.ipynb](https://github.com/OliverShao/POMCP/blob/main/src/plot_evaluation_data.ipynb) is created to plot the undiscounted return in results.
