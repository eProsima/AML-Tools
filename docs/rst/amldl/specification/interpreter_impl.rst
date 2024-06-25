.. include:: /rst/exports/roles.include

.. _amldl_specification_interpreter_impl:

#################################
AML-DL Interpreter Implementation
#################################

A viable implementation consists of a few commands implemented as functions of a base language like Python or C++.
Using a base language has obvious advantages as the entire base language is available to add control loops, variables, etc.
Relying on a base language makes the implementation simpler as it makes unnecessary to use a parser or a lexer.

A single descriptor object can be used for the commands' input and output.
AML-DL commands correspond to functions of the base language that take one or many descriptor objects and return a descriptor object.
It is enough with a few types of descriptor objects: type ``CONST``, type ``SET``, type ``VECTOR``, type ``CVECTOR``, type ``TVECTOR``, and type ``DUPLE``.

Descriptors of type ``CONST`` correspond to constants defined using the command :math:`C` while descriptors of type ``CVECTOR`` correspond to vectors of constants returned by the command :math:`CV`.

The return values of commands :math:`C`, :math:`CV` , :math:`INC`, and :math:`EXC` are final descriptors, in the sense that they are appended to the program output.
The program output is comprised of a set of descriptors of type ``CONST`` and a set of descriptors of type ``DUPLE``.
Other commands, like :math:`M` , :math:`S`, :math:`T` , :math:`V` , or :math:`R` return descriptors that are not appended to the program output and that are meant to be used as inputs of other commands or assigned to a variable.
In other words, these commands return descriptors that should be bound.
Hence, descriptors are either final or bound.
The binding of a descriptor to an input parameter of a command may occur directly or by means of a variable of the base language.

At any point, the program state corresponds to a set of final descriptors collected so far, and a dictionary that maps names to descriptor objects.
Names are regular character string that can be used to invoke descriptor objects by name.
The find command F is provided to specifically retrieve a descriptor by name although, for convenience, names can always be used instead of descriptor objects as parameters of any command.

The command :math:`V([name])`, which declares a vector, produces a descriptor that can be optionally bound.
As a side effect, and only if a name is provided, a newly created empty vector is associated with said name.
It returns a descriptor of type ``VECTOR``.

Descriptors of type ``SET`` are returned by the commands :math:`M` and :math:`S`.
A ``SET`` descriptor corresponds to a set of constants.
When a ``VECTOR`` or ``CVECTOR`` is provided as an input to :math:`M` or :math:`S` their components are added to the returned set.
The :math:`M` command, which corresponds to the idempotent operator, adds every provided parameter to the returned set.
These sets are going to be interpreted as the component constants of terms, so they will become elements of the semilattice.

Descriptors of type ``DUPLE`` correspond to duples and can be positive when produced by the :math:`INC` command, or negative when produced by the :math:`EXC` command.
Type ``DUPLE`` descriptors are always final.
The :math:`INC` and :math:`EXC` commands require inputs of type ``SET``.

The iterator command :math:`T` provides indexing capabilities and makes the language significantly more flexible.
It can operate with any other command.
The iterator command changes descriptors of type ``SET``, ``VECTOR`` or ``CVECTOR`` into descriptors of type ``TVECTOR``.
When a command has an input of type ``TVECTOR``, the command is applied not to the ``TVECTOR`` itself but to each one of its components.
The function then returns a ``TVECTOR`` whose components are the corresponding returned values.

A command may receive one or many inputs of type ``TVECTOR``.
Descriptors of type ``TVECTOR`` have an index number.
If a command receives more than one input of type ``TVECTOR`` with the same index the components are replaced at the same time in all of them.
In this case, all the ``TVECTOR`` descriptors with the same index should have the same dimension otherwise an error is returned.
For example, a command that receives one or many descriptors of type ``TVECTOR`` of size n and the same index returns a ``TVECTOR`` of size :math:`n`.
When a command receives more than one input of type ``TVECTOR`` with different indexes the output corresponds to a ``TVECTOR`` with components of type ``TVECTOR`` producing a tree of depth equal to the number of different indexes used.
For example, if a command receives two descriptors of type ``TVECTOR`` with sizes :math:`m` and :math:`n` then it produces a ``TVECTOR`` of size m whose components are descriptors of type ``TVECTOR`` of size n, therefore producing a total of :math:`m \times n` applications of the command.

Descriptors form a tree.
We have just mentioned the case of nested descriptors of type ``TVECTOR``.
Descriptors of type ``DUPLE`` consist of a pair of references to descriptors of type ``SET``, one to the left and the other to the right-hand descriptors.
Descriptors of type ``VECTOR`` have components of any type except ``DUPLE``.
