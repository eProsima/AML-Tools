.. include:: /rst/exports/roles.include

.. _amldl_specification_examples:

#############
Code Examples
#############

Example 1
*********

In this first example, two vectors of :math:`n` constants, :math:`black` and :math:`white`, are defined and the independence of each constant with the rest is provided as a set of negative constraints.
Iterator command :math:`T` is used twice with the same index :math:`i` resulting in a coordinated replacement.
The following code returns the two ``CVECTORs`` of :math:`n` constants.

.. code-block:: python

    CV('black', n)
    CV('white', n)

For instance, if :math:`n=3`, the code defines the constants:

.. math::

    black[0], black[1], black[2], white[0], white[1], white[2]

These ``CVECTORs`` are used below to define two sets of negative duples with:

.. code-block:: python

    EXC(T('black', i), M('white', R('black', T('black', i))))
    EXC(T('white', i), M('black', R('white', T('white', i))))

which results in the following duples:

.. math::

    & black[0] \nleq white[0] \odot white[1] \odot white[2] \odot black[1] \odot black[2] \\
    & black[1] \nleq white[0] \odot white[1] \odot white[2] \odot black[0] \odot black[2] \\
    & black[2] \nleq white[0] \odot white[1] \odot white[2] \odot black[0] \odot black[1] \\
    & white[0] \nleq black[0] \odot black[1] \odot black[2] \odot white[1] \odot white[2] \\
    & white[1] \nleq black[0] \odot black[1] \odot black[2] \odot white[0] \odot white[2] \\
    & white[2] \nleq black[0] \odot black[1] \odot black[2] \odot white[0] \odot white[1]

Example 2
*********

The next example makes a random selection of constants from :math:`black` and calculates its idempotent summation.
For each constant not selected in :math:`black`, the corresponding constant in :math:`white` is appended to the summation so exactly :math:`n` constants are always added.
The resulting element for the summation is assigned to the right-hand side of a positive duple.
First, we define the constants, and set the :math:`black` and :math:`white` ``CVECTORs`` as being complementary component by component,

.. code-block:: python

    n = 3
    C('r')
    CV('black', n)
    CV('white', n)
    COMP('black', 'white')

then we carry out a random selection of components of :math:`black` that get stored in a descriptor :math:`x` of type VECTOR, and use :math:`x` to define a positive duple with the code:

.. code-block:: python

    p = 0.05
    atLeastOne = False
    notAll = True
    x = SOME('black', p, atLeastOne, notAll)
    INC('r', M(x, R('white', COMP(x))))

A possible return for :math:`x` could have components :math:`black[0], black[1]` and the positive duple would then be:

.. math::

    r \leq black[0] \odot black[1] \odot white[2]

With the recent changes it is simple to define real-valued fields:

.. code-block:: python

    C('cold')
    C('warm')
    INC('cold', N('temperature', 8))
    INC('warm', N('temperature', 25))

This will return a series of constants representing the field and its value:

.. math::

    & cold \leq tempL8 \odot tempR8  \\
    & warm \leq tempL25 \odot tempR25
