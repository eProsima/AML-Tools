.. include:: /rst/exports/roles.include

.. _amldl_consistency_checker:

##########################
AML-DL Consistency Checker
##########################


AML is a machine learning method that relies on calculating semantic embeddings into algebras with idempotent operators such as semilattices.
The user should describe the ML problem at hand using a set of algebraic order equations and inequations.
These equations are referred as the embedding and the solutions of the embedding as the model.
If the set of equations has at least one solution then the embedding is said to be consistent.
Inconsistent embeddings have no solutions, i.e. they have no representation as semilattice models.

The *AML-DL Consistency Checker (AML-DL-CC)* is a software tool to study the consistency of algebraic semantic embeddings into semilattices.
The AML-DL-CC can determine if an embedding expressed in AML-DL is consistent or not.
In case the embedding is inconsistent, the AML-DL-CC pinpoints the potential primary source of the inconsistency and the possible secondary sources.
The primary source is a negative duple that cannot be satisfied because it contradicts other duples of the embedding.
The AML-DL-CC will indicate the AML-DL instruction from which said negative duple originates.
To help understand how the inconsistency arises, the AML-DL-CC also shows the AML-DL instructions that produce duples which, collectively or individually, contradict the primary source duple.
If the embedding contains more than one inconsistency the AML-DL-CC will find and display all of them.

Further details about semantic embeddings are provided in section :ref:`AML Description Language (AML-DL) <amldl_specification>` of this documentation.

Components of the AML-DL-CC
***************************

The AML-DL-CC combines an interpreter and an analyzer:

* An interpreter for AML-DL that transforms AML-DL code into a set of positive and negative duples.
* An analyzer that uses these duples to determine if there is at least one semilattice model compatible with them.

If there is at least one semilattice model that satisfies all the duples then the code is considered consistent.

The AML-DL interpreter
=======================

The AML-DL specification is presented in section :ref:`AML Description Language (AML-DL) <amldl_specification>`.
The interpreter fully implements that specification, transforming the AML-DL instructions into a set of duples.
Those duples represent order relations, with each duple describing the element on its left-hand side, its right-hand side, and whether such order relation is positive (:math:`<`), or negative (:math:`\nless`).

The consistency analyzer
========================

The methodology and mathematics necessary to determine the consistency of an embedding are described in *Section 2.6 Trace and trace constraints* of  `Algebraic Machine Learning <https://arxiv.org/pdf/1803.05252>`__ paper.

In this section, two directed graphs are used: one containing the constants (minimum units to describe the components of the problem) and the terms (idempotent summation of constants); and a second one, the dual, that mirrors the first graph with reverted relations. The dual contains constants and atoms but not terms as every term in the master algebra has a constant as its dual.
A model for the dual is first created making use of the positive and negative duples from the interpreter.
The edges of the graphs are established using the following steps.

* The first step is to satisfy the reverted negative relations, :math:`\nless`. This may involve adding some dual-of-atoms to the dual graph.
* Reverted positive relations, :math:`<`, are also satisfied by simply adding the necessary edges and using transitive closure of the graph.
* After transitive closure, all reverted relations are satisfied if and only if the embedding is consistent.

To determine the consistency of an embedding, the AML-DL-CC implicitly calculates the dual. The
embedding is consistent if it can build a model for the dual until the end.
