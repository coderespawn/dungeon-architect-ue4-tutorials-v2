Advanced Theming
================

.. figure:: /images/wip.png
   :align: center


Selection Rules
---------------

One way to select the node in a theme graph is by setting the probablity.  If you want more control, you can write you own selection logic in a script

Example #1
^^^^^^^^^^
Different tiles for rooms and corridors


Example #2
^^^^^^^^^^

In this example the towers are too crowded and close to each other.

.. figure:: /images/tutorial/07/01.jpg
   :align: center


A selector rule is created to select alternate cells

.. figure:: /images/tutorial/07/02.jpg
   :align: center

.. figure:: /images/tutorial/07/03.jpg
   :align: center



.. code-block:: c#

	using UnityEngine;
	using System.Collections;
	using DungeonArchitect;

	public class AlternateSelectionRule : SelectorRule {
		public override bool CanSelect(PropSocket socket, Matrix4x4 propTransform, DungeonModel model, System.Random random) {
			return (socket.gridPosition.x + socket.gridPosition.z) % 2 == 0;
		}
	}

	


Transform Rules
---------------

A transform rule lets you apply an offset using a script. These are great for randomization or handling any special case of object alignment through script


