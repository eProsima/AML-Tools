.. include:: /rst/exports/roles.include

.. _amldl_interpreter_architecture:

###############################
AML-DL Interpreter Architecture
###############################

The output of the AML-DL Interpreter is comprised of a set of descriptors representing constants, and a set of duples, which are formed by a pair of sets of descriptors.
Descriptors can contain constants or other nested descriptors, giving rise to a tree structure.
As the leaves of this tree structure are always formed by constants, duples can in essence be assimilated to a pair of sets of constants.

Commands are either final or bound.
Commands are final if their return descriptors are directly appended to the embedding's output.
These commands are ``C``, ``CV``, ``ADD``.
Commands are bound if their return descriptors are not appended to the embedding's output.
These descriptors are meant to be used as inputs for other commands and bound to the output at a later step.

At any point, the program state corresponds to a set of final descriptors collected so far, and an internal dictionary that maps names to descriptor objects.
Names are regular character strings that can be used to invoke descriptor objects by name.
