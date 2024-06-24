.. include:: /rst/exports/roles.include

.. _amldl_command_set:

###########
Command Set
###########

Constant creation
*****************

.. list-table::
   :widths: 18 82

   * - **C(name)**
     - Defines a constant with the given name.
       Returns a descriptor of type ``CONST`` that cannot be bound.
   * - **CV(name, n)**
     - Defines a vector of constants with names: :math:`name[0], name[1], ..., name[n-1]`.
       Returns a descriptor of type ``CVECTOR`` of length `n` that cannot be bound.
   * - **V([name])**
     - Defines an empty vector.
       Optional parameter :math:`name` assigns a name to the vector.
       Returns a descriptor of type ``VECTOR`` that can be optionally bound.
   * - **F(name[,i])**
     - Finds a descriptor with the given name.
       Optional parameter :math:`i` is an integer.
       :math:`name` should refer to a descriptor of type ``CONST``, ``VECTOR``, or ``CVECTOR``.
       Returns the descriptor associated with the name.
       Returns the :math:`i-th` component of the descriptor associated to the :math:`name`, if :math:`i` is given and the descriptor is of type ``VECTOR`` or ``CVECTOR``.

Real-valued field usage and declaration
***************************************

.. list-table::
   :widths: 15 85

   * - **N(field, v)**
     - If is the first use of the parameter `field` it declares a new real-valued numeric field.
       Generates a descriptor for the value `v` of the numeric field `field`.
       Returns a descriptors of type ``SET``.

Duple creation
**************

.. list-table::
   :widths: 15 85

   * - **INC(l, h)**
     - Defines a positive duple :math:`l \leq h`.
       :math:`l` and :math:`h` are descriptors or descriptor names of any type except type ``DUPLE``.
       Returns a final descriptor of type ``DUPLE`` or ``TVECTOR`` that cannot be bound.
   * - **EXC(l, h)**
     - Defines a negative duple :math:`l \nleq h`.
       :math:`l` and :math:`h` are descriptors or descriptor names of any type except type ``DUPLE``.
       Returns a final descriptor of type ``DUPLE`` or ``TVECTOR`` that cannot be bound.

Term formation and manipulation
*******************************

The arguments :math:`p_i` in the following commands are descriptors or the names assigned to descriptors.

.. list-table::
   :widths: 18 82

   * - **M(p[, ...])**
     - Calculates an idempotent summation.
       The argument or arguments :math:`p` are descriptors of any type except of type ``DUPLE``.
       Returns a descriptor of type ``SET``.
       If some argument is of type ``TVECTOR``, :math:`M` returns a descriptor of type ``TVECTOR`` whose components are of type ``SET``.
       The return value should be bound.
   * - **APP(p, pa)**
     - Appends pa to :math:`p`.
       Argument :math:`p` should be of type ``VECTOR``.
       Modifies :math:`p`.
       No return value.
   * - **R(p, pr)**
     - Removes :math:`pr` from a copy of the vector :math:`p`.
       If argument :math:`pr` is an integer, removes the :math:`pr-th` component.
       Argument :math:`p` is not modified.
       Argument :math:`p` is of type ``VECTOR`` or ``TVECTOR``.
       Returns a descriptor of the same type as :math:`p` that should be bound.
   * - **CMP(p1, p2)**
     - Declares :math:`p1` and :math:`p2` as the logical negation of each other.
       :math:`p1`, :math:`p2` are of type ``CONST`` or ``CVECTOR`` of the same length.
       Operates component-wise if :math:`p1`, :math:`p2` are ``CVECTORS``.
       No return value.
   * - **CMP(p)**
     - Finds or calculates a descriptor that is the complementary of p.
       :math:`p` is a descriptor of type ``CONST``, ``CVECTOR``, or ``TVECTOR``.
       Copies :math:`p` recursively, replacing every ``CONST`` descriptor with its complementary.
       The argument :math:`p` is not modified.
       Returns a descriptor of the same type as :math:`p`.
   * - **T(p[, i])**
     - Associates an iterator to :math:`p`.
       The argument :math:`p` is of any type except ``DUPLE``.
       The optional parameter :math:`i` is an integer that identifies the iterator.
       Returns a descriptor of type ``TVECTOR`` that should be bound.

Auxiliary commands
******************

.. list-table::
   :widths: 25 75

   * - **HEADER(name)**
     - Guards a section of the program that should be read just once.
       Returns :math:`True` when :math:`HEADER(name)` has not been read yet.
   * - **SOME(p, prob[, atLeastOne, notAll])**
     - Randomly chooses items with a probability :math:`prob`.
       Default values for optional parameters are :math:`False`.
       Boolean parameter:math: `atLeastOne` ensures at least one item is selected.
       Boolean parameter:math: `notAll` makes sure not all the items are selected.
       The argument:math: `p` is a descriptor, or the name assigned to a descriptor, of type ``VECTOR``, ``CVECTOR``, or ``TVECTOR``.
       Returns a descriptor of the same type as :math:`p`.
   * - **REGION(n)**
     - Assignes duples defined after the statement to region :math:`n`, where:math: `n` is a positive integer.
       The default region is 0.
       The assigned value remains unaltered until ``REGION`` is set to a different value.


Additional commands for unmanaged base languages
************************************************

.. list-table::
   :widths: 10 90

   * - **^p**
     - Prevents the deletion of a descriptor p.
   * - **/p**
     - Returns the memory of a preserved descriptor :math:`^p`.

