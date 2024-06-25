.. include:: /rst/exports/roles.include

.. _amldl_overview:

########
Overview
########

Semilattices
************

Semilattices have a single operation, the idempotent operation :math:`\odot`, from which we can derive an order relation :math:`\leq`.
We will have to rely only on these two operations to build our embeddings.
Although the number of operations is small, we can have access to an unlimited supply of *constants*.
The meaning of the order relation and idempotent operator may be different when different constants are involved.
The constants thus increase the descriptive power of the idempotent operator.

A constant of an algebra is an element that has a name, so we refer to elements with a name as *constants*.
Constants act as primitives for the embedding and their meaning is a key part of the *interpretation*.
The embedding typically starts by selecting a set of constants and choosing one or many meanings for the order relation and the idempotent operator.

To illustrate how constants can modulate the meaning of the order relation suppose that we have constants *a* and *b* that refer to two people.
We could choose the order relation to mean "*is a son of*" and write :math:`a < b` to describe *a as a son of b*.
That is possible but it will leave us without syntactic tools to refer to other family relationships.
Instead, we can use additional constants *son, daughter, uncle* and use :math:`a < b \odot son` or :math:`a < b \odot uncle` to modify the meaning of the order relation.
Order relationships can also be negative.
We can say :math:`a \nleq b \odot daughter` to say that *a is not the daughter of b*.
Every element mentioned in an embedding should be either a constant or an idempotent summation of constants.
By putting constants together with the idempotent operator every element can be formed.
Elements can be seen as sets of constants.
However, two (or more) different sets of constants may yield the same element or may be related by the order relation even if one is not a subset of the other.
We refer to pairs of elements related by the order relation as *positive duples* and to the pairs of elements related by the negation of the order relation as *negative duples*.

Language
********

AML-DL commands declare constants, construct elements by putting constants together, or specify order relationships between pairs of elements.
In addition to these basic operations, AML-DL v0.2 has a flexible system of indexing and iteration that allows for a single statement to describe entire families of duples of the same sign.

AML-DL Grammar
==============

.. math::

    & ⟨const\_decl⟩ ::= 'C(' ⟨ID⟩ ')' \\
    & ⟨const\_vec\_decl⟩ ::= 'CV(' ⟨ID⟩ ',' ⟨INT ⟩ ')' \\
    & ⟨vec decl⟩ ::= 'V(' ⟨ID⟩ ')' \\
    & \qquad | 'V()' \\
    & ⟨it\_decl⟩ ::= 'T(' ⟨descr⟩ ')' \\
    & \qquad | 'T(' ⟨descr⟩ ',' ⟨INT⟩ ')' \\
    & ⟨cmp\_create⟩ ::= 'CMP(' ⟨comp\_create\_arg⟩ ',' ⟨comp\_create\_arg⟩ ')' \\
    & ⟨comp\_create\_arg⟩ ::= ⟨const\_decl ⟩ \\
    & \qquad | ⟨const\_vec\_decl⟩ \\
    & \qquad | 'F(' ⟨ID⟩ ')' \\
    & \qquad | 'F(' ⟨ID⟩ ',' ⟨INT⟩ ')' \\
    & ⟨cmp\_get⟩ ::= 'CMP(' ⟨cmp\_get\_arg⟩ ')' \\
    & ⟨cmp\_get\_arg⟩ ::= ⟨const\_decl⟩ \\
    & \qquad | ⟨const\_vec\_decl⟩ \\
    & \qquad | ⟨it\_decl⟩ \\
    & \qquad | 'F(' ⟨ID⟩ ')' \\
    & \qquad | 'F(' ⟨ID⟩ ',' ⟨INT⟩ ')' \\
    & ⟨descr⟩ ::= 'F(' ⟨ID⟩ ')' \\
    & \qquad | 'F(' ⟨ID⟩ ',' ⟨INT⟩ ')' \\
    & \qquad | ⟨it\_decl⟩ \\
    & \qquad | ⟨m\_expr⟩ \\
    & \qquad | ⟨const\_decl⟩ \\
    & \qquad | ⟨const\_vec\_decl⟩ \\
    & \qquad | ⟨vec\_decl⟩ \\
    & \qquad | ⟨cmp get⟩ \\
    & ⟨incl⟩ ::= 'INCL(' ⟨descr⟩ ',' ⟨descr⟩ ') \\
    & ⟨excl⟩ ::= 'EXCL(' ⟨descr⟩ ',' ⟨descr⟩ ') \\
    & ⟨m expr⟩ ::= 'M(' ⟨m params⟩ ')' \\
    & ⟨m params⟩ ::= ⟨m params⟩ ',' ⟨descr⟩ \\
    & \qquad | ⟨descr⟩ \\
    & ⟨iterable⟩ ::= ⟨const\_vec\_decl⟩ \\
    & \qquad | ⟨vec\_decl⟩ \\
    & \qquad | ⟨it\_decl⟩ \\
    & \qquad | 'F(' ⟨ID⟩ ')' \\
    & ⟨some cmd⟩ ::= 'SOME(' ⟨iterable⟩ ',' ⟨FLOAT⟩ ',' ⟨BIN⟩ ',' ⟨BIN⟩ ') \\
    & ⟨region cmd⟩ ::= 'REGION(' ⟨INT⟩ ')' \\
    & ⟨header cmd⟩ ::= 'HEADER(' ⟨ID⟩ ')' \\
    & ⟨add\_v⟩ ::= 'APP(' ⟨descr⟩ ',' ⟨descr⟩ ')' \\
    & ⟨remove\_v⟩ ::= 'R(' ⟨descr⟩ ',' ⟨descr⟩ ')' \\
    & \qquad | 'R(' ⟨descr⟩ ',' ⟨INT⟩ ') \\
    & ⟨save\_cmd⟩ ::= 'ˆ' ⟨descr⟩ \\
    & ⟨free\_cmd⟩ ::= '/' ⟨descr⟩ \\
    & ⟨statement⟩ ::= ⟨const decl⟩ \\
    & \qquad | ⟨const\_vec\_decl⟩ \\
    & \qquad | ⟨vec\_decl⟩ \\
    & \qquad | ⟨cmp\_create⟩ \\
    & \qquad | ⟨incl⟩ \\
    & \qquad | ⟨excl⟩ \\
    & \qquad | ⟨some\_cmd⟩ \\
    & \qquad | ⟨region\_cmd⟩ \\
    & \qquad | ⟨header\_cmd⟩ \\
    & \qquad | ⟨add\_v⟩ \\
    & \qquad | ⟨remove\_v⟩ \\
    & \qquad | ⟨save\_cmd⟩ \\
    & \qquad | ⟨free\_cmd⟩ \\
    & ⟨statement\_seq⟩ ::= ⟨statement\_seq⟩ ⟨statement⟩ \\
    & \qquad | \epsilon \\
    & ⟨program⟩ ::= ⟨statement seq⟩

AML-DL Commands
***************

AML-DL v0.1 data types are constants, vectors of constants, elements, vectors of elements, duples, and vectors of duples.

*   :math:`T`.
    Vectors may or may not be indexed. Indexed vectors result from the application of the iterator command :math:`T`.

*   :math:`C(name)` and :math:`CV(name, n)`.
    These commands define a constant and a vector of constants of length :math:`n`, respectively.

*   :math:`F(name)`.
    To retrieve the elements of a vector of constants by name, we use the find operator :math:`F(name)`.

*   :math:`APP(v, e)`.
    Vectors of elements can be defined as :math:`v = V([name])` and can be built by appending elements using :math:`APP(v, e)` that appends :math:`e` to vector :math:`v`.

*   :math:`M(p1, p2, ...)`.
    To calculate the idempotent operation we can use the command :math:`M(p1, p2, ...)` where :math:`p1, p2, ...` are constants.

*   :math:`T(v)`.
    Indexing and iterating along a vector can be done with the help of the iterator command :math:`T(v)`.
    For example, assume :math:`v` is a vector with elements :math:`v[0], v[1], ..., v[n-1]`.
    Then :math:`M(T(v), e)` produces a vector :math:`v[0] \odot e, v[1] \odot e, ..., v[n-1] \odot e`.
    Iterators can have one or many indexes associated to them.
    An index is identified by a positive whole number.
    For example, if :math:`v` and :math:`w` are vectors of the same size, :math:`M(T(v, 1), T(w, 1), e)` returns vector :math:`v[0] \odot w[0] \odot e, v[1] \odot w[1] \odot e, ..., v[n-1] \odot w[n-1] \odot e`, a vector of size :math:`n`.
    We now assume that :math:`w` has size :math:`m`.
    If we use different indexes, :math:`M(T(v, 1), T(w, 2), e)` returns :math:`v[0] \odot w[0] \odot e, v[0] \odot w[1] \odot e, ..., v[0] \odot w[m-1] \odot e, ..., v[1] \odot w[0] \odot e, ...,` |br|:math:`v[n-1] \odot w[m-1] \odot e`, a vector of size :math:`n \times m`.

*   :math:`INC(a, b)` and :math:`EXC(a, b)`

    Positive and negative duples are defined using :math:`INC(a, b)` and :math:`EXC(a, b)` respectively, which directly translates into :math:`a \leq b` and :math:`a \nleq b`.
    The iterator command associates indexes that remain after a command is applied.
    For example :math:`INC(a, M(T(v), e))` produces the vector of :math:`n` duples: :math:`a \leq v[0] \odot e, a \leq v[1] \odot e, ..., a \leq v[n-1] \odot e`.
    If we invoke :math:`INC(T(w, 1), M(T(v, 1), e))` assuming vector :math:`v` and :math:`w` have the same size then we obtain the vector of :math:`n` duples: :math:`w[0] \leq v[0] \odot e, w[1] \leq v[1] \odot e, ..., w[n-1] \leq v[n-1] \odot e`.
    Accordingly, using different indexes, :math:`INC(T(w, 2), M(T(v, 1), e))` will produce :math:`n \times m` positive duples: :math:`w[0] \leq v[0] \odot e, w[0] \leq v[1] \odot e, ..., w[0] \leq v[n-1] \odot e, w[1] \leq v[0] \odot e, ...,` |br|:math:`w[m-1] \leq v[n-1] \odot e`.

*  :math:`R(v, d)`.
   Auxiliary command that removes component :math:`d` from a copy of vector :math:`v`.

*  :math:`SOME(v, p)`.
   Auxiliary command that produces a vector with components chosen at random from vector :math:`v` with probability :math:`p`.

*  :math:`CMP(p1, p2)`.
   Auxiliary command that declares a bidirectional map between objects :math:`p1` and :math:`p2` such that :math:`CMP(p1)` returns :math:`p2` and :math:`CMP(p2)` returns :math:`p1`. :math:`CMP` acts component-wise if :math:`p1` and :math:`p2` are vectors of the same size.
