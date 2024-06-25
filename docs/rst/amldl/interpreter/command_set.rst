.. include:: /rst/exports/roles.include

.. _amldl_interpreter_command_set:

##############################
AML-DL Interpreter Command Set
##############################

Loading AML-DL command set
**************************

The functions and classes of the AML-DL Interpreter are defined in the module ``aml.amldl``.
They can be individually imported with the following commands:

.. code-block:: python

    from aml.amldl import(
        load_embedding,
        Descriptor,
        ADD, APP, C, CMP, CV, E, EXC, F, HEADER,
        INC, M, R, S, SOME, T, V
    )

In this section, it is assumed that they are all imported into the main namespace with:

.. code-block:: python

    from aml.amldl import *

Embedding creation
******************

Most functions need to be called from within a Python Context that represents an embedding.
An embedding is an instance of the class ``Descriptor``.

.. code-block:: python

    with Descriptor() as theEmbedding:
        ...

All examples below are assumed to be executed within such a Python Context.
All duples are assigned the region of their embedding at the time they are created.
The ``REGION`` property of the embedding can be modified at any point.

.. code-block:: python

    with Descriptor() as theEmbedding:
    theEmbedding.REGION = 5

Constant creation
*****************

*   **C(name)**

    Defines a constant with the given name.

    .. code-block:: python

        C('Q')

*   **CV(name, n)**

    Defines a vector of constants with names: name[0], name[1], ..., name[n-1].

    .. code-block:: python

        CV('Q', 10)

*   **V([name])**

    Defines an empty vector.

    .. code-block:: python

        V('Qx')
        APP(F('Qx'), V())

Duple creation
**************

*   **INC(left term, right term)**

    Defines a positive duple :math:`l \leq h`.
    :math:`l` and :math:`h` cannot be duples.

    .. code-block:: python

        ADD(INC('U', 'B'))

*   **EXC(left term, right term)**

    Defines a negative duple :math:`l \nleq h`.
    :math:`l` and :math:`h` cannot be duples.

    .. code-block:: python

        ADD(EXC('Qx', 'Qy'))

Term creation and manipulation
==============================

*   **APP(p, a)**

    Appends :math:`a` to :math:`p`, where :math:`p` is of type vector.
    The vector :math:`p` is modified in place.

    .. code-block:: python

        # Create a vector that contains two empty vectors
        V('Qx')
        APP(F('Qx'), V())
        APP(F('Qx'), V())

*   **M(p_1, ..., p_n)**

    Returns :math:`a` set containing the :math:`p_1` to :math:`p_n` elements.
    If any argument is of type :math:`tvector`, returns a descriptor of type :math:`tvector` whose components are sets.

    .. code-block:: python

        M(Qx, Qy, B, U )

*   **R(p, r)**

    Removes :math:`r` from the vector :math:`p`.
    If :math:`r` is an integer, removes the :math:`r`-th element of :math:`p`.
    Returns a new vector, and :math:`p` is not modified.

    .. code-block:: python

        b = CV('black', 2)
        w = CV('white', 2)
        wb [0] = M(w, R(b, 0) ) # w [0], w [1], b [1]
        wb [1] = M(w, R(b, 1) ) # w [0], w [1], b [0]

*   **CMP(p1, p2)**

    Declares :math:`p1` and :math:`p2` as the logical negations of each other.
    Operates component-wise if :math:`p1` and :math:`p2` are vectors of the same length.
    No return value.

    .. code-block:: python

        CV('Q', 5)
        CV('E', 5)
        CMP('Q', 'E')

*   **CMP(p)**

    Finds or calculates the complementary of :math:`p`.
    Returns a copy of :math:`p` where every element is substituted by its complementary.

    .. code-block:: python

        CV('Q', 5)
        CV('E', 5)
        CMP('Q', 'E')
        F('E') == CMP('Q')

*   **T(p [,i])**

    Associates an iterator to :math:`p`, where :math:`p` cannot be a duple.
    The optional parameter :math:`i` is an integer that identifies the iterator.
    Returns a :math:`tvector`.

    .. code-block:: python

        b = CV('black', 2)
        w = CV('white', 2)
        wb = M(w, R(b, T(b)))
        # wb.t[0] = M(w, R(b, 0)) = w[0], w[1], b[1]
        # wb.t[1] = M(w, R(b, 1)) = w[0], w[1], b[0]

Auxiliary commands
==================

*   **F(name [,i])**

    Returns the descriptor associated with name.
    If :math:`i` is given and :math:`p` is a vector, return the :math:`i-th` element of :math:`p`.

    .. code-block:: python

        CV('black', 5)
        b3 = F('black', 3)

*   **SOME(p, prob [,atLeastOne, notAll])**
    Randomly chooses items from :math:`p` with a probability :math:`prob` per element.
    When set to *True*, the flags ensure that there is at least one element, and not all have been chosen, respectively.
    By default, they are set to *False*.

    .. code-block:: python

        CV('black', 5)
        SOME('black', 0.5)

*   **HEADER(name)**

    Guards a section of the embedding that should be read just once.
    Returns *True* the first time, *False* otherwise.

    .. code-block:: python

        if HEADER('black constants'):
            CV('black', 5)

Loading an embedding
====================

The embedding can be wrapped in a function embedding that takes any number of input arguments, that can be used as parameters, and returns the embedding's output.

.. code-block:: python

    def embedding ():
        with Descriptor() as theEmbedding:
            C('A')
            C('B')
            ADD(INC('A', 'B'))

            constantNames = [el.key for el in F(theEmbedding.PEND_TRANSF).r]
            p = F(theEmbedding.INCLUSIONS).r
            n = F(theEmbedding.EXCLUSIONS).r

        return (constantNames, p, n)

From a different script the embedding can be loaded using the ``load_embedding`` function.

.. code-block:: python

    from aml.amldl import load_embedding
    (constantNames, p, n) = dl.load_embedding("path/to/embedding.py")
