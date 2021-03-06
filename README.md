# AWS2C

## Introduction

The Adventure Writing System (AWS) is a tool put together by Aristide Torrelli 
to easily write interactive fiction games.

Aristide describes his tool here: http://www.aristidetorrelli.it/aws3/Avventure.html

I thought it would have been fun to put together a converter that creates
a standard C source from the files produced by the AWS tool.

## Install

To compile the tool, you will need `gcc` and the `make` utility installed in
your system. If you use a Unix operating system, most probably it is the case.
If you use Windows, you may find Cygwin helpful.

Just download the source archive and type `make`. That will create the `aws2c` executable.

## Basic usage

Once you have the executable `aws2c` in your path, you use it as in the
following example:

`aws2c adventure.aws adventure.c`

where `adventure.aws` contains the game in the AWS format and the `adventure.c`
is the generated file. To compile it, you will need the `aws.h`, `inout.c`,
`inout.h` and `systemd.h` files, provided with the tool:

`gcc adventure.c inout.c -o adventure`

to obtain an executable called `adventure`.

An example of a file that can be renamed as `systemd.h` and used for compiling
games to modern Unix terminals is `modern.h`.

For the moment AWS2C does not cover all the full range of actions, decisions
and functions offered by Aristide's AWS 3.2 system. If the tool encounters
something it does not recognise, it will give an error and the resulting C file
may not be compilable. Other actions are just ignored but a warning message
is generated while running `aws2c`.

## Command line options

Since one of the design goals of the utility was to obtain files that can be
compiled for old Commodore machines (C64, C128, Plus4, etc...), options for
translating UTF-8 characters are available. The program help should explain them:

~~~~
$ ./aws2c -h
Adventure Writing System to C compiler, version 1.0
Davide Bucci 2018

Usage: ./aws2c [options] inputfile.aws outputfile

then compile (along with file inout.c) using your favourite C compiler.

Available options:
 -h  this help
 -u  convert UTF-8 characters into standard ASCII chars.
        è -> e   é -> e
 -r  same as -u, but keep accents as separate chars.
        è -> e'  è -> e`
 -s  same as -u, but only employs the single accent '.
        é -> e'  è -> e'
 -c  compress text with Huffman algorithm.
 -d  employ 6 directions instead of 10.
 -m  employ hardcoded messages instead of an array.
 -n  do not clear the screen every time a new room is shown.
  --verbose write plenty of things.
~~~~

If you have a machine that only has the accent ' available such as a Commodore 64, it makes sense to use the `-s` option to create the file to be compiled.
The `-m` option deserves some discussion. The default way of storing messages in the generated C code is an array of structures. This allows a certain flexibility for example to show a message with a code calculated on the fly during the game. With the `-m` option this is not possible as there will be a bunch of variables called `message1`, `message2` etc. This saves space at the expense of a (rarely used) flexibility. If a calculated message code is exploited in the AWS file you are trying to convert with the `-m` option, you will get errors during the compilation of the generated file.

## Some examples

This tool comes with some examples. In each sub-folder, you find a readme file with all the instructions.

### Dawn patrol

This game is an English translation of "Pattuglia all'alba", adapted by A. Torrelli from a type-in BASIC program.

### La piramide di Iunnuh

This game was published as a type-in BASIC program for the TI99/4A by Aristide Torrelli (MCmicrocomputer 33, sett. 1984) and then ported to the ZX Spectrum by Manlio Severi (MCmicrocomputer 35, nov. 1984). It was one of the very fist Italian adventure games and it had a certain success at the time.

It was originally written in Basic, but Aristide decided in 2014 to write a version in AWS that I am using here as an example.

By the way, basing myself from the original published BASIC version of the game, I converted it in Java in 2011 and in C in 2018. I also translated the game in English. I did this before developing `aws2c` and you can find the result of my efforts here: http://davbucci.chez-alice.fr/index.php?argument=varie/innuh/innuh.inc&language=English

### La piramide di Iunnuh 2

This is a much longer and deep adventure game that A. Torrelli did in 2014 for the thirtieth anniversary of his first game. I translated it in English and it's an example of how you can 

### 
