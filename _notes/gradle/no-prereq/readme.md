---
layout: post
title: "Gradle and GNU Make: No-prerequisite, build a single file"
date: 2016-04-10
---

# Gradle and GNU Make: No-prerequisite, build a single file

This document compares the ability of GNU Make and Gradle with regards
to building a single output file. Three typical actions are considered:

* the initial build
* the incremental build
* post-build modifications to the build

## GNU Make

```cmake
outputfile.txt:
        echo "content" >$@
```

### Initial build:

```
$ make
echo "content" >outputfile.txt
```

### Incremental build:

```
$ make
make: 'outputfile.txt' is up to date.
```

### Post-build modifications:

```
$ echo "more" >>outputfile.txt
$ make
make: 'outputfile.txt' is up to date.
```

Make does not rebuild the target if it already exists (and because
it only look at timestamps of pre-requisites which are not present in
this example).

## Gradle

While GNU Make only tracks whether the output file exists or not when
there are not prerequisites, Gradle has the ability to track the file
existence and the file contents.

```groovy
task outputFileName() {
    // We declare the file using new File()
    // It is also possible to use the build-in file() method:
    // def outputFile = file('outputFile.txt')
    def outputFile = new File('outputFile.txt')
    outputs.file outputFile
    doLast {
        println "Writing content to file ${outputFile.name}"
        outputFile.write("content\n")
    }
}
```

### Initial build:

```
$ gradle --daemon outputFileName
:outputFileName
Writing content to file outputFile.txt

BUILD SUCCESSFUL

Total time: 0.526 secs
```

### Incremental build:

```
$ gradle --daemon outputFileName
:outputFileName UP-TO-DATE

BUILD SUCCESSFUL

Total time: 0.511 secs
```

### Post-build modifications:

```
$ echo "more" >>outputFile.txt
$ gradle --daemon outputFileName
:outputFileName
Writing content to file outputFile.txt

BUILD SUCCESSFUL

Total time: 0.527 secs
```

Gradle does rebuild the target (task output) when it is altered by
an external program. This is because Gradle caches a hash of the file
content and uses it to detect file changes.
