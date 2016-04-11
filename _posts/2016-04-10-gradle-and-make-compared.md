---
layout: post
title: "Gradle and GNU Make Compared"
date: 2016-04-10
---

# Gradle and GNU Make compared

I'd like to compare Gradle to GNU Make.

## No pre-requisite

<table>
<tr>
<td>
   <pre lang="cmake">
   outputfile:
           echo "content" &gt;outputfile.txt
   </pre>
</td>
<td>
  <pre lang="groovy">
  apply plugin: 'base'

  task outputFile() {
      def outputFile = file('outputFile.txt')
      outputs.file outputFile
      doLast {
          println 'Writing content to file'
          outputFile.write("content\n")
      }
  }
  </pre>
</td>
<td>
  Variables defined with <code>def</code> cannot be changed once defined. This is similar to <code>readonly</code> or <code>const</code> in C# or <code>final</code> in Java. Most variables in Nemerle aren't explicitly typed like this.
</td>
</tr>
</table>

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
