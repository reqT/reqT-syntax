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

1. [Optional] If you have changed the metamodel of reqT, regenerate the ```reqT-flex-clauses.txt``` using the command ```reqt -j``` and insert the reqT flex clauses in the ```ReqTTokenGenerator.flex``` file (look for comments on ENTITY TYPES etc in the file to find what to replace).
2. Run ```jflex ReqTTokenGenerator.flex``` to re-generate ```ReqTTokenGenerator.java```
3. Patch by hand the new ```ReqTTokenGenerator.java``` file according to the instructions in ```how-to-patch.txt```
4. Put the patched ReqTTokenGenerator in the src/... lib (replace the old one)
5. Run ```ant``` to build a new ```rsyntaxtextarea.jar```
6. Put the ```rsyntaxtextarea.jar``` file in your reqT repo under reqT/lib
7. Build reqT according to instructions in the [main reqT repo](https://github.com/reqT/reqT) 
