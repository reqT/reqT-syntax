reqT-highlight
==============

Syntax highlighting lib for reqT based on RSyntaxTextArea and JFlex. Many thanks to those projects!
The repo is used to build a customized rsyntaxtextarea.jar that is a lib used by reqT.


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

1. [Optional] If you have changed the metamodel of reqT, regenerate the ´´reqT-flex-clauses.txt´´ using the command ´´reqt -j´´ and paste the output into ´´reqT-flex-clauses.txt´´ file. Then insert the reqT flex clauses in the ReqTTokenGenerator.flex file.
2. run ´´jflex´´  ReqTTokenGenerator.flex to generate ReqTTokenGenerator.java
3. Patch by hand the ReqTTokenGenerator according to the instructions in how-to-patch.txt
4. Put the patched ReqTTokenGenerator in the src/... lib (replace the old one)
5. run ´´ant´´ to build a new rsyntaxtextarea.jar
6. put the rsyntaxtextarea.jar file in your reqT repo under reqT/lib
7. build reqT according to instructions in the main reqT repo 
