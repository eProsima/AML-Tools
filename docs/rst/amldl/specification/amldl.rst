.. include:: /rst/exports/roles.include

.. _amldl_specification:

#################################
AML Description Language (AML-DL)
#################################

The word *embedding* is often used as a synonym of encoding.
However, an embedding has a precise mathematical definition; an embedding is a structure-preserving map that allows to identify a mathematical structure within another.
An example of structure-preserving maps is an injective homomorphism of a group A into another group B.
For such identification to be possible, A has to be a subgroup of B and only then the homomorphism is an embedding.
Mathematicians have extended this notion into something more general.
An embedding of A into B can be defined even when A and B are very different mathematical entities with different properties and operations.
For example, a group can be embedded within a graph.
This concept is known to mathematical logicians as *semantic embedding*.

In a semantic embedding, there is the notion of *interpretation*.
An interpretation is a mathematical Rosetta Stone that explains how to see A inside of B.
We could say that while a regular encoding relies entirely on the interpretation, in the case of a semantic embedding that is not necessarily the case.
In the example of the subgroup, it is clear that A had to be there, inside of B, from the very beginning.
In this case, the interpretation is only a function that locates A within B.

From regular encodings to homomorphisms there is a range of many possible structure-preserving maps.
Suppose we take a novel and encode it into a string of zeros and ones to store it in our computer memory.
The interpretation explains how to read letters from the zeros and ones, how to form words with the letters and how to understand the words.
Without the interpretation, there is little left from the novel into the string of zeros and ones.
If instead of a single novel we encode all the volumes of the national library, we may increasingly be able to deduce a larger portion of the meaning of the string of zeros and ones, and with enough corpus, we may be able to reconstruct the missing interpretation or some equivalent interpretation.
The encoding of the novel has left too much meaning up to the interpretation so a larger additional corpus is necessary to decipher it.

If instead of a novel we encode a computer program into a string of zeros and ones we may be able to deduce an interpretation from a much shorter bit string.
This is because the interpretation of the programming language is simpler than the interpretation of the novel.
In a semantic embedding, we try to find an interpretation that is as simple as possible.
Rather than encoding A into B using a fixed interpretation, a semantic embedding consists in finding A into B by discovering an appropriate interpretation.

Searching for an appropriate (simple and accurate) interpretation of A into B is a natural problem that we, humans, are not so familiar with.
When we communicate an object A to a listener B using English we start with a language and its interpretation shared between the speaker and B.
The communication with B occurs with an interpretation that is mostly fixed.
The goal of the Algebraic Machine Learning Description Language (AML-DL) is to communicate with a very simple listener B, a semilattice.
Semilattices live in Plato's world and we do not share with them a language.
On the other hand, their simple structure allows us to understand them so well that it becomes possible to find simple interpretations for any A.


.. toctree::
   :maxdepth: 2

   /rst/amldl/specification/overview
   /rst/amldl/specification/interpreter_impl
   /rst/amldl/specification/command_set
   /rst/amldl/specification/examples
