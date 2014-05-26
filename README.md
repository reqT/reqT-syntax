reqT-syntax
==============

Syntax highlighting lib for reqT based on [RSyntaxTextArea](http://fifesoft.com/rsyntaxtextarea/) and [JFlex](http://jflex.de/). Many thanks to those excellent projects!
The repo is used to build a customized rsyntaxtextarea.jar to be used as a lib for [reqT](https://github.com/reqT/reqT).


How to build
============

The build process is a bit tricky as it involves manual patching of a generated lexer source file. It involves updating the grammar (if desired), then generating the lexer using jflex, then building the rsyntaxttextarea.jar, then putting that jar in the reqT repo and rebuild reqT. Detailed instructions follows.

Prerequisites
--------------
Install these applications first if you don't have the already:
* Java JDK to compile the code
* JFlex to generate token generator
* Apache Ant to build the project


Steps
-------

1. If you have changed the metamodel of reqT inside reqT, regenerate the ```reqT-flex-clauses.txt``` using the command ```reqt -j```
2. Insert the new ```reqT-flex-clause.txt``` clauses in the ```ReqTTokenGenerator.flex``` file (look for comment ```/* reqT BEGIN */``` in the file to find what to replace).
3. Run ```jflex ReqTTokenGenerator.flex``` to generate a new [ReqTTokenGenerator.java]( https://github.com/reqT/reqT-syntax/blob/master/ReqTTokenMaker.java)
4. Patch by hand the generated ReqTTokenGenerator.java file according to the instructions in [how-to-patch.txt](https://github.com/reqT/reqT-syntax/blob/master/how-to-patch-ReqTTokenMaker.java.txt)
5. Put the patched ReqTTokenGenerator.java in this dir by replacing the old one: [src\org\fife\ui\rsyntaxtextarea\modes](https://github.com/reqT/reqT-syntax/tree/master/src/org/fife/ui/rsyntaxtextarea/modes) 
Copy-replace in your desktop or use commands in terminal similar to:

        rm src/org/fife/ui/rsyntaxtextarea/modes/ReqTTokenMaker.java
        mv ReqTTokenMaker.java src/org/fife/ui/rsyntaxtextarea/modes/.
    
6. Run ```ant``` to build a new ```rsyntaxtextarea.jar```  (ignore the 4 deprecation warnings)
7. Put the [dist/rsyntaxtextarea.jar](https://github.com/reqT/reqT-syntax/tree/master/dist) file in your reqT repo under [reqT/lib](https://github.com/reqT/reqT)
8. Build reqT according to instructions in the [main reqT repo](https://github.com/reqT/reqT) 
