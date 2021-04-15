# POMCP

### Compile
Run make to compile

### Run RockSample game
In src, for example, run ```./pomcp --problem rocksample --size 11 --number 11 --timeout 10000 --maxdouble 15 --rolloutknowledge 2 --outputfile ro_s11_n11_maxDouble15_GenerateSimplePolicy_GoToEachRock.txt``` This will simulate the game on a 11x11 board with 11 rocks.

--rolloutknowledge == 4 is running on multiple policies using Switch-Case.
--rolloutknowledge == 2 is running on ONE policy.(By Default, it runs GeneratePreferred() ).
