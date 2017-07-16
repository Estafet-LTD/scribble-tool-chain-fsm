# scribble-tool-chain
General Stuff:
The scribble tools chain repo is an eclipse project that takes dot notation, generated from the Scribble compiler, and makes the dot FSM both easier to read and morphs it into an FSM config file that can be used as input to the fsmdemo project (see link below).

We use antlr to parse the dot files (hence the DOTGrammar.g4). The source is in two packages, the first is the grammar.grammar package which has the generated antlr artefacts and the main for the translator. The grammar.workingmemory have some classes used to create an abstract model for a FSM that are then used in the generation of a pretty dot file and an FSM config file.

Using it in eclipse:
I have set up my eclipse to do some basic tests with a few run configurations for "help", "-easyFSM" and "-dot" which you use to test it out. The output in each case is on the console. If you wish you can copy/paste the output into a file. For example if you use "dot" copy/paste into a file called authorisersvc.dot then you can invoke graphviz from the command line as follows and look at the png generated:

	dot -Tpng authorisersvc.dot >output.png

The main scribble example is SupplierProtocol in the scribble-examples folder. You don't need it to test stuff. Rather you need test-data/authorsersvc.dot which is generated by the scribble compiler directly. If you need to generate more then you need to do something akin to:

	scribblec ScribbleFile -fsm ProtocolName roleName >test-data/roleName.dot

In some other window, saving the output into the test-data folder and refresh eclipse. As a concrete example you might try:

	scribblec SupplierProtocol.scr -fsm Suppliers requestor >test-data/requestor.fsm

Deployment:
Easiest way to deploy is as follows:

Export the build as fmsxlator.jar into the runtime-folder/lib folder overwriting what is there already.

Export the entire runtime-folder to a target folder. Setup the SCRIBBLEDIR to point to the target folder.

Running:
Use this in conjunction with the fsmdemo project. But start here to generate all that is need to actually run the distributed system described in some scribble file.

For the example in the runtime-folders under scribble-examples/supplier you can generate all that is needed to run the example as a distributed system by doing the following:

	deploy ../scribble-examples/supplier/SupplierProtocol.scr Suppliers ../generated/supplier-example <role names>

This will generate everything into ../generated/supplier-example.
 
 More succinctly the invocation is of the form:

	deploy scribble-file protocol-name target-folder list-of-roles

The deploy script leverages the scribble compiler (which is in an entirely different repo owned by Dr Ray Hu) and which is included in this repo as a set of jar files. It also wraps the fsmxlate and the dot (graphviz) facility that takes a dot file and turns it into a png. You can download dot from http://www.graphviz.org/Download.php.

All of the scripts in the runtime-foler/bin can be invoked with -h or --help to see more info.





