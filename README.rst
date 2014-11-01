========================================
Remote Access System
========================================

A rsh-like access system

This is my homework of Network Programming (for graduate student) in 2014.
(still a undergraduate student then)

Spec
========================================

- The length of a single-line input will not exceed 10000 characters
- There may be huge number of commands in a single-line input
- Each command will not exceed 256 characters
- There must be one or more spaces between commands and symbols (or arguments.), but no spaces between pipe and numbers
	* ``cat hello.txt | number``
	* ``cat hello.txt |1 number``
- There will not be any '/' character in demo input
- Pipe ("|") will not come with "printenv" and "setenv"
- Use '% ' as the command line prompt

- welcome message

  ::

      ****************************************
      ** Welcome to the information server. **
      ****************************************

- Close the connection between the server and the client immediately when the server receive "exit"
- Note that the forked process of server MUST be killed when the connection to the client is closed.  Otherwise, there may be lots zombie processes
- If there is command not found, print as follows:

  ::

      Unknown command: [command].

- ``|N`` means the stdout of last command should be piped to next Nth legal process, where ``1 <= N <= 1000``
- If there is any error in a input line, the line number still counts

  ::

      % ls |1
      % ctt               <= unknown command, process number is not counted
      Unknown command: [ctt].
      % number
      1	bin/
      2	test.html

      % ls |1 ctt   		<= if find any process illegal, process will stop immediately
      Unknown command: [ctt].
      % cat               <= this command is first legal process after "ls |1"
      bin/
      test.html

- We will use pipe or numbered-pipe after unknown command like "ls |1 ctt | cat" or "ls |1 ctt |1". In this case, process will stop when running unknown command, so the command or numbered-pipe after unknown command will not execute and numbered-pipe will not be counted.

  ::

      % ls |1 ctt | cat   <= cat will not execute and numbered-pipe will not be counted.
      Unknown command: [ctt].
      % cat
      bin/
      test.html

- If mutiple commands output to the same pipe, the output should be ordered, not mixed.

  ::

      % ls |3 removetag test.html |2 ls |1 cat   <= cat will not execute and numbered-pipe will not be counted.
      bin/
      test.html

      Test
      This is a test program
      for ras.

      bin/
      test.html

- There must be "ls", "cat", "removetag", "removetag0", "number” in "bin/" of “ras/“.
- You have to execute the files in "bin/" with an "exec()"-based function.(eg. execvp() or execlp() ...)

Feature
========================================

Problem
========================================
