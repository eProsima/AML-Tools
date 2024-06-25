.. include:: /rst/exports/roles.include

.. _amldl_interpreter:

##################
AML-DL Interpreter
##################

The primary goals of Algebraic Machine Learning Description Language (AML-DL) are to give the user the capability to concisely describe elaborate algebraic semantic embeddings and to establish a methodology to build embeddings for real-life problems.
Please refer to the :ref:`AML-DL Specification <amldl_specification>` for more information.

The AML-DL Interpreter implements the AML-DL Specification into an interpreter that can transform human-readable semantic embeddings into AML input data for the AML Engine.


The AML-DL Interpreter is provided in the form of a Python module and strictly follows the AML-DL Specification.
Using a base language such as Python has obvious advantages as the entire base language is available as a platform to add control flow, variable handling, etc.
Relying on a base language also makes the implementation simpler as it makes unnecessary to use a parser or a lexer.
Python has the additional advantage of being well-maintained, easy to use, and widely used in data science and machine learning.

The implementation of AML-DL, as described in the specification, is highly customizable, but also instructions perform relatively simple operations.
This can lead to the repetition of certain instructions and the appearance of common patterns.
The use of a base language can help with code reusability as these repeated instructions and patterns can be grouped into functions and classes.
In the future, if certain patterns are common to a wide range of problems, they can be added to the AML-DL Python module.

This section describes the architecture and usage of the AML-DL Interpreter.
The commands that the interpreter provides are described, and examples of use are provided for each individual one, together with example embeddings for its use.


.. toctree::
   :maxdepth: 2

   /rst/amldl/interpreter/architecture.rst
   /rst/amldl/interpreter/command_set.rst
