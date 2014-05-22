reqT-syntax
==============

Syntax highlighting lib for reqT based on [RSyntaxTextArea](http://fifesoft.com/rsyntaxtextarea/) and [JFlex](http://jflex.de/). Many thanks to those projects!
The repo is used to build a customized rsyntaxtextarea.jar to be used as a lib for [reqT](https://github.com/reqT/reqT).


How to build
============

The build process is a bit tricky as it involves manual patching of a generated lexer source file, but it basically involves updating the grammar (if desired), then generating the lexer using jflex, then building the rsyntaxttextarea.jar, then putting that jar in the reqT repo and rebuild reqT. Detailed instructions follows.

Prerequisites
--------------
Install these applications first:
* JFlex to generate token generator
* Apache Ant to build the project
* Java JDK to compile the code


Steps
-------

1. If you have changed the metamodel of reqT inside reqT, regenerate the ```reqT-flex-clauses.txt``` using the command ```reqt -j```
2. Insert the new ```reqT-flex-clause.txt``` clauses in the ```ReqTTokenGenerator.flex``` file (look for comment ```/* reqT BEGIN */``` in the file to find what to replace).
3. Run ```jflex ReqTTokenGenerator.flex``` to re-generate ```ReqTTokenGenerator.java```
4. Patch by hand the new ```ReqTTokenGenerator.java``` file according to the instructions in ```how-to-patch.txt```
5. Put the patched ReqTTokenGenerator.java in this dir by replacing the old one: [src\org\fife\ui\rsyntaxtextarea\modes](https://github.com/reqT/reqT-syntax/tree/master/src/org/fife/ui/rsyntaxtextarea/modes) 
6. Run ```ant``` to build a new ```rsyntaxtextarea.jar```
7. Put the ```rsyntaxtextarea.jar``` file in your reqT repo under reqT/lib
8. Build reqT according to instructions in the [main reqT repo](https://github.com/reqT/reqT) 
