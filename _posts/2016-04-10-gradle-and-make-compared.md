---
layout: post
title: "Gradle and GNU Make Compared"
date: 2016-04-10
---

# Gradle and GNU Make compared

I'd like to compare Gradle to GNU Make.

## No-prerequisite, build a single file

GNU Make:

```cmake
outputfile.txt:
        echo "content" >$@
```

Execution:

```
$ make
echo "content" >outputfile.txt
$ make
make: 'outputfile.txt' is up to date.
```

Gradle:

```groovy
apply plugin: 'base'

task outputFile() {
    def outputFile = file('outputFile.txt')
    outputs.file outputFile
    doLast {
        println 'Writing content to file'
        outputFile.write("content\n")
    }
}
```

Execution:

```
$ gradle --daemon outputFile
:outputFile
Writing content to file

BUILD SUCCESSFUL

Total time: 0.515 secs
$ gradle --daemon outputFile
:outputFile UP-TO-DATE

BUILD SUCCESSFUL

Total time: 0.523 secs
```

### Comment

Both, as expected, only build the output file when it does not exist.
The GNU Make code is short. The Gradle code is long and verbose.

## No pre-requisite, build an empty directory

Change directory timestamp.

## No pre-requisite, build a directory with files in it

Change directory content: remove or add a file. Does gradle empty the directory? Does it remove spurious files.

Change file content in directory. Does gradle empty the dir when it determines it needs to run again?

## Single directory pre-requisite

## Single file pre-requisite

Here is an svg file, shold be below this line:

![Alt text](/images/square.svg)

And here is a code snippet:

```java
String calc(String str) {
    return str+"yay"
}
```

And a link to [code](https://gist.github.com/martinda/ab1c3a2445bb202356d6)

And embeded code:
<script src="https://gist.github.com/martinda/ab1c3a2445bb202356d6.js"></script>

Embeded code with syntax highlight:
<script src="https://gist.github.com/martinda/59ed5f0b2e89e802c410.js"></script>
