**Aims**

This assignment aims to give you:
- practice in Shell programming generally
- a clear concrete understanding of Git's core semantics
Note: the material in the lecture notes will not be sufficient by itself to allow you to complete this assignment. You may need to search on-line documentation for Shell, Git, etc. Being able to search documentation efficiently for the information you need is a very useful skill for any kind of computing work.

**Introduction**

Your task in this assignment is to implement Shrug, a subset of the version control system Git.

Git is a very complex program which has many individual commands. You will implement only a few of the most important commands. You will also be given a number of simplifying assumptions, which make your task easier.

Shrug is a contraction of Shell-running-git.

You must implement Shrug in Shell.

Interestingly, early versions of Git made heavy use of Shell and Perl.

**Reference Implementation**

Many aspects of this assignment are not fully specified in this document; instead, you must match the behaviour of a reference implementation.

For example, your script shrug-add should match the behaviour of 2041 shrug-add exactly, including producing the same error messages.

Provision of a reference implementation is a common method to provide or define an operational specification, and it's something you will likely need to do after you leave UNSW.

Discovering and matching the reference implementation's behaviour is deliberately part of the assignment.

While the code in the reference implementation is fairly straight forward, reverse-engineering its behaviour is obviously not so simple, and is a nice example of how coming to grips with the precise semantics of an apparently obvious task can still be challenging.

If you discover what you believe to be a bug in the reference implementation, report it in the class forum. Andrew may fix the bug, or indicate that you do not need to match the reference implementation's behaviour in this case.

**Shrug Commands**

***Subset 0***

Many aspects of this assignment are not fully specified in this document; instead, you must match the behaviour of a reference implementation.

For example, your script shrug-add should match the behaviour of 2041 shrug-add exactly, including producing the same error messages.

Provision of a reference implementation is a common method to provide or define an operational specification, and it's something you will likely need to do after you leave UNSW.

Discovering and matching the reference implementation's behaviour is deliberately part of the assignment.

While the code in the reference implementation is fairly straight forward, reverse-engineering its behaviour is obviously not so simple, and is a nice example of how coming to grips with the precise semantics of an apparently obvious task can still be challenging.

If you discover what you believe to be a bug in the reference implementation, report it in the class forum. Andrew may fix the bug, or indicate that you do not need to match the reference implementation's behaviour in this case.

****shrug-init****

The shrug-init command creates an empty Shrug repository.

shrug-init should create a directory named .shrug, which it will use to store the repository. It should produce an error message if this directory already exists.

You should match this, and other error messages exactly. For example:

```
$ ls -d .shrug
ls: cannot access '.shrug': No such file or directory

$ shrug-init
Initialized empty shrug repository in .shrug

$ ls -d .shrug
.shrug

$ shrug-init
shrug-init: error: .shrug already exists
shrug-init may create initial files or directories inside .shrug.
```

You do not have to use a particular representation to store the repository.

You do not have to create the same files or directories inside shrug-init as the reference implementation.

****shrug-add filenames...****
The shrug-add command adds the contents of one or more files to the index.

Files are added to the repository in a two step process. The first step is adding them to the index.

You will need to store files in the index somehow in the .shrug sub-directory. For example, you might choose store them in a sub-directory of .shrug.

Only ordinary files in the current directory can be added. You can assume filenames start with an alphanumeric character ([a-zA-Z0-9]) and will only contain alpha-numeric characters, plus '.', '-' and '_' characters.

The shrug-add command, and other Shrug commands, will not be given pathnames with slashes.

****shrug-commit -m message****
The shrug-commit command saves a copy of all files in the index to the repository.

A message describing the commit must be included as part of the commit command.

Shrug commits are numbered sequentially: they are not hashes, like Git. You must match the numbering scheme.

You can assume the commit message is ASCII, does not contain new-line characters, and does not start with a '-' character.

****shrug-log****
The shrug-log command prints a line for every commit made to the repository: each line should contain the commit number, and the commit message.

****shrug-show [commit]:filename****
The shrug-show should print the contents of the specified filename as of the specified commit. If commit is omitted, the contents of the file in the index should be printed.

You can assume the commit if specified will be a non-negative integer.

For example:
```
$ ./shrug-init
Initialized empty shrug repository in .shrug

$ echo line 1 > a
echo hello world >b

$ ./shrug-add a b

$ ./shrug-commit -m 'first commit'
Committed as commit 0

$ echo  line 2 >>a

$ ./shrug-add a

$ ./shrug-commit -m 'second commit'
Committed as commit 1

$ ./shrug-log
1 second commit
0 first commit

$ echo line 3 >>a

$ ./shrug-add a

$ echo line 4 >>a

$ ./shrug-show 0:a
line 1

$ ./shrug-show 1:a
line 1
line 2

$ ./shrug-show :a
line 1
line 2
line 3

$ cat a
line 1
line 2
line 3
line 4

$ ./shrug-show 0:b
hello world

$ ./shrug-show 1:b
hello world
```
