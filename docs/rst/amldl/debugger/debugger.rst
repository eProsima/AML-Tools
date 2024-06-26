.. include:: /rst/exports/roles.include

.. _amldl_debugger:

###############
AML-DL Debugger
###############

AML is a new AI paradigm that combines user-defined symbols with self-generated symbols.
This permits AML to learn from the data and adapt to the world as neural networks do, combined with the power for explainability of Symbolic AI.
AML is a purely symbolic approach and neither uses neurons nor is a neuro-symbolic method.
AML does not use parameters and it does not rely on fitting, regression, backtracking, constraint satisfiability, logical rules, production rules, or error minimization.

The user should describe the ML problem at hand using a set of constants, that represent concepts, and a set of algebraic order equations and inequations, in the form of positive and negative duples, that represent relationships between subsets of concepts.
These equations are referred to as the embedding, and the solutions of the embedding as the model.
If the set of equations has at least one solution the embedding is said to be consistent.
Inconsistent embeddings have no solutions, i.e. they have no representation as semilattice models.
Further detail about semantic embeddings is provided in section :ref:`amldl_interpreter` of this documentation.

The AML-DL Debugger is a software tool to visualize semantic embeddings and some of their properties.
Currently the AML-DL Debugger can

* organize and display the embedding constants,
* display positive and negative duples using their given name instead of their indices,
* study and explore embedding consistency,
* be extended to implement new modules.

These properties allow for a quick feedback loop when developing or modifying semantic embedding using AML Description Language (AML-DL).

.. figure:: /rst/figures/amldl_debugger.png
    :align: center

Components of the AML-DL Debugger
*********************************

The AML-DL Debugger combines a user interface and a module loader:

* A Text User Interface (TUI) that displays several options in text view, so it can easily be used in remote machines or from a docker container.
* A module loader that allows for new tools to be easily added.