# OS-system_calls-library_functions

## To Run Project

1. Go into project directory
2. Type in 'make'
3. ./reverse [-h] [-i inputFileName] [-o outputFileName]

The goal of this project is to become familiar with the environment in opsys while practicing system calls. You will also demonstrate your proficiency in the use of perror and getopt in this submission. Additionally, you should understand the different steps of compilation and linking. This project is just reading some integers from an input file and writing them out in reverse order into the output file. All that is required of you is to use fork(), parsing the options, and using perror().

### Task

Your project should consist of one program, which will fork versions of itself to do some file processing. It will start by using
some command line arguments. You must implement at least the following command line arguments using getopt:

-h
-i inputfilename
-o outputfilename

The -h option will display all legal command line options and how it is expected to run, as well as the default behavior. If input and output filenames are not specified, the defaults should be input.dat and output.dat. Once you have parsed the command line arguments and validated them, then you should attempt to open the input file. The input file should start with a number on a line by itself, with that number indicating the amount of times you will be required to do a task with copies of your process using fork. Each task list will follow in the file, which will consist of an integer on one line (representing the amount of numbers that will follow) and that many numbers. An example of this input file is below:

3

6

3 6 107 8 1 3

4

1 3 50 4

7

5 3 5 7 8 9 1

The above file indicates 3 sets (first line) with the first set containing 6 integers, the second set containing 4 integers, and the third set containing 7 integers. The main process (parent) should read the first line of the file. Once it has read that line, it should then go into a loop based on that number, with each iteration of the loop forking off a copy that will then process the next two lines. Once that child has finished its work (defined below), it will write some data to the output file and then terminate. At that point, as the parent detects its child has terminated, it should do another iteration of the loop until done. After all children have terminated. the parent should write the process IDs (PIDs) of all of its children that it launched, as well as its own PID to the output file. When a child process starts, it should read the next line of the file, which will tell it how many numbers to read afterwards. We see in our example file that the first forked child would read a 6. It should then read that number of integers and put them into a stack. After putting all of the numbers into a stack, the child should write its PID to the output file, followed by those numbers in reverse order. For example:

13278: 3 1 8 107 6 3

After this has been done with the example file given above, we would expect an output file to look as below (with different PIDs, of course):

13278: 7 3 1 8 107 6 3

13281: 4 50 3 1

13294: 1 9 8 7 5 3 5

All children were: 13278 13281 13294

Parent PID: 13250

I’ll like some meaningful error messages. The format for error messages should be:

reverse: Error: Detailed error message

where reverse is actually the name of the executable (argv[0]) that you are trying to execute. These error messages should be sent to stderr. Any errors generated due to system calls should be reported using perror with the same format.

Here is the set of tasks after you have your code compiled.

1. Run your program and observe the results for different number of processes.
2. Report if the number of integer on a line does not match the expected number that was specified on the previous line.

### Invoking the solution
Your solution will be invoked using the following command:

reverse [-h] [-i inputfilename] [-o outputfilename]

If a user specifies -h, please print the usage message and terminate. If the user does not specify an input file, use the default name for the input file. If the user does not specify an output file, create the filename by appending .out to the input file name. Please make use of perror after each system call to report any error messages. With the use of perror, I’ll like some meaningful error messages. The format for error messages should be as specified earlier.
It is required for this project that you use version control (git), a Makefile, and a README. You should check in a version of your code at each step of exercise, at the minimum into your git repository. Your README file should consist, at a minimum, of a description of how I should compile and run your project, any outstanding problems that it still has, and any problems you encountered. Your Makefile should use suffix-rules or pattern-rules and have an option to clean up object files.
