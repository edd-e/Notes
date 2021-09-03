# Bash shell scripts<!-- omit in toc -->

Bash scripting notes.

## Table of contents<!-- omit in toc -->

- [Introduction](#introduction)
- [Output](#output)
- [Comments](#comments)

## Introduction

Bash scripts are executed in a shell or command-line interpreter. The script can have a file extension or none; for example `script.sh` or `script`.

The beginning of the file must specify a path to the interpreter of the script:

```sh
!# /bin/sh
```

## Output

You can use `echo` to display output

```sh
echo 'This message will appear in the console'
```

## Comments

Comments are marked with the `#` symbol.

```sh
# This is a single line comment
```

Multi-line comments are denoted with the here document feature.

```sh
echo 'This message will appear in the console'
<<AnyNameHere
echo 'This message will not appear in the console'
This is a comment area.
Lines here are not executed.
AnyNameHere
echo 'This message will also appear in the console'
```
