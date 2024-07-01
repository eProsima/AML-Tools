.. include:: /rst/exports/alias.include
.. include:: /rst/exports/roles.include

.. _amlip_user_manual:

###########
User Manual
###########

.. _amlip_scenarios:

Scenarios
=========

The |amlip| framework is divided in different **scenarios** or **use cases**
that allow it to exploit all the capabilities :term:`AML` has to offer.
These scenarios work independently of each other and make sense separately,
but can be seamlessly combined to create a more complex network.
Each of the scenarios rely on a different set of **Nodes** that perform the different actions required.

For more infromation, check the AML-IP Scenarios sections:

* `Monitor Network State Scenario <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/scenarios/monitor_state.html>`__
* `Workload Distribution Scenario <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/scenarios/workload_distribution.html>`__
* `Collaborative Learning Scenario <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/scenarios/collaborative_learning.html>`__
* `Distributed Inference Scenario <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/scenarios/distributed_inference.html>`__

.. _amlip_nodes:

Nodes
=====

An |amlip| network is divided in independent stand-alone individuals named :term:`Nodes <Node>`.
A Node, understood as a software piece that performs one or multiple :term:`Actions <Action>` in a auto-managing way,
does not require external orchestration neither a central point of computation.
These actions can be local actions such as calculations, data process, algorithm executions, etc.,
or communication actions as send messages, receive data, wait for data or specific status, etc.
Each Node belongs to one and only one :term:`Scenario`.

There are different ways to run or to work with a Node.
Some of them are applications that can be executed and perform a fixed action.
Others, however, require a user interaction as specifying the action such Node must perform depending on its status
and the data received.
In this last case, the Nodes are programming *Objects* that can be instantiated and customized regarding the
action that must be performed.

For more information, check the AML-IP Nodes sections:

* `Agent Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/agent.html>`__
* `Status Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/status.html>`__
* `Main Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/main.html>`__
* `Computing Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/computing.html>`__
* `Edge Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/edge.html>`__
* `Inference Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/inference.html>`__
* `Model Manager Receiver Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/model_manager_receiver.html>`__
* `Model Manager Sender Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/model_manager_sender.html>`__

.. _amlip_tools:

Tools
=====

Agent Tool
----------

This tool launches an `Agent Node <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/nodes/agent.html>`__, which is the node in charge of communicating a local node or AML-IP cluster with the rest of the network in :term:`WAN`\s.
It centralizes the :term:`WAN` discovery and communication, i.e. it is the bridge for all the nodes in their :term:`LAN`\s with the rest of the AML-IP components.

For more information, check the `AML-IP Agent tool section <https://aml-ip.readthedocs.io/en/latest/rst/user_manual/tools/agent.html>`__.
