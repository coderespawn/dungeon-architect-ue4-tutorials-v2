Grid Builder
============
 
The `Grid Builder` generates a dungeon by scattering rooms across the map and connecting them with corridors.  This builder supports height variations (stairs)

.. figure:: /images/tutorial/F/01.jpg
   :align: center

We've used this dungeon builder in the previous section :doc:`create_first_dungeon` and :doc:`design_first_theme`

In this section, we'll explore more on this builder

Properties
^^^^^^^^^^

Continuing on the map created in the section :doc:`design_first_theme`, open the map and select the `Dungeon` actor and inspect the properties

.. figure:: /images/tutorial/F/02.png
   :align: center

* Change the ``Seed`` parameter to build a different dungeon layout
* Set the ``Grid Cell Size`` parameter according to your moduler art asset. If the ground mesh is 400x400 and the stair mesh height is 200, set this to ``(400, 400, 200)``
* The dungeon creation method first creates a number of cells (defined by ``NumCells``) and spreads them across the scene.  
* The size of these cells is define by the parameters ``Min Cell Size`` and ``Max Cell Size``
* Some of these cells will be promoted to Rooms and the rest will be promoted to Corridors.  If the cell area is large enough (parameter ``Room Area Threshold``), that cell is promoted to a `Room`, otherwise a `Corridor`
* The rooms are connected together with corridors
* Control how much height variation is allowed with ``Height Variation Probability``
* A new Stair will not be created between two tiles if there's another stair nearby that if traversed, takes N steps to reach this cell. This value is controlled by ``Stair Connection Tollerance``.  Bump this number up if you want fewer stairs
* Maximum allowed stair: Determine how high a stair tile can get.  If set to one, the builder will create stairs that go only one level up
* Both Rooms and Corridors have a ``Ground`` marker.   Rooms are surrounded by ``Wall`` markers while the corridors are surrounded by ``Fence`` marker


Platform Volume
^^^^^^^^^^^^^^^
Platform Volumes let you control the placement of the rooms or corridors.   You do this dropping in a ``Grid Dungeon Platform Volume`` on to the scene and resizing  / positioning it on the scene and you room will be built around it.


.. figure:: /images/tutorial/F/03.png
   :align: center


.. figure:: /images/tutorial/F/04.jpg
   :align: center
   
Select the PlatformVolume game object, set the Dungeon reference and enable ``Realtime Update`` (or press Rebuild Dungeon)

.. figure:: /images/tutorial/F/05.png
   :align: center

Change the Cell Type from `Corridor` to `Room`

.. figure:: /images/tutorial/F/06.gif
   :align: center
   
   Platform Volume to create a Corridor or a Room

Move the `Platform Volume` and scale it to control the position and size of your room. You can have multiple platform volumes in the scene. Check the samples in the Launch Pad for more examples


Theme Override Volume
^^^^^^^^^^^^^^^^^^^^^

Theme Override Volumes let you apply another theme on certain portions of your dungeons that are covered by this volume.  These are useful for adding variations to your dungeons. 


Navigate to ``Asset/DungeonArchitect/Prefabs`` and drag drop the ``ThemeOverrideVolume`` prefab on to the scene

.. figure:: /images/tutorial/F/09.png
   :align: center
   

Move and scale it to cover a certain portion of the dungeon


.. figure:: /images/tutorial/F/07.jpg
   :align: center

   
Select the theme override volume you just dropped and inspect the properties and assign the DungeonGrid reference

.. figure:: /images/tutorial/F/10.png
   :align: center

Assign a theme you'd like to apply within these bounds.  Then hit ``Rebuild Dungeon`` button

.. figure:: /images/tutorial/F/08.jpg
   :align: center
   
.. figure:: /images/tutorial/F/11.gif
   :align: center
   
   Before / After theme override


Paint Mode
^^^^^^^^^^

You can paint your own dungeon layout on top of the procedural dungeon

Select the Dungeon Edit Mode from the Modes panel.  This will allow you to use the various paint tools to draw over the existing layout

.. figure:: /images/tutorial/F/12.png
   :align: center
   
``Left click`` and drag to draw dungeon cells.   ``Shift + Left click`` to delete cells.   ``Scroll wheel`` to move the cursor up/down

.. figure:: /images/tutorial/F/13.gif
   :align: center
   





