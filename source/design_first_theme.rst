Design your first theme
=======================

A theme file is a mapping between **marker** names (like Walls, Ground, Door etc) and the meshes that you provide.    The prefabs you map here will be used to build your dungeon

.. figure:: /images/tutorial/02/theme_editor_preview.jpg
   :align: center
   
   
In the previous section, we created a dungeon with an existing theme file (CandyDungeonTheme).  In this section, we'll create one ourselves

Create a Theme File
-------------------

Create a new theme file from either the Main menu or the Create menu

.. figure:: /images/tutorial/02/create_theme_01.png
   :align: center
   
   Create from Main menu
   
.. figure:: /images/tutorial/02/create_theme_02.png
   :align: center
   
   Create from Create menu
  

This will create a theme file in the current open directory in the Projects window

.. figure:: /images/tutorial/02/03.png
   :align: center
   

Open the Theme File
-------------------

Double-click the theme file to open the **Theme Editor**.  Dock the theme editor so you can see both the Scene view and the Theme Editor at the same time

.. figure:: /images/tutorial/02/04.jpg
   :align: center
   
   
Assign the Theme File
---------------------

Destroy the existing dungeon by selecting ``DungeonGrid`` game object and click ``Destroy Dungeon`` button


Assign the theme file that you just created, on to the DungeonGrid game object

.. figure:: /images/tutorial/02/05.png
   :align: center
   

Click ``Build Dungeon`` and nothing should appear.   That's because we haven't added prefab mappings on the theme yet



Design the Theme
----------------

Navigate to ``Assets\DungeonArchitect_Samples\Demo_Theme_Candy\Prefabs``.  This folder contains a set of mesh prefabs we can use for our dungeon

.. figure:: /images/tutorial/02/06.jpg
   :align: center
   
Add Ground
^^^^^^^^^^

Drag-drop the ground prefab mesh on to the Theme Editor

.. figure:: /images/tutorial/02/07.jpg
   :align: center
   

Link up the mesh node with the ``Ground`` marker node.  When you do, you should see a live preview on the scene view with the dungeon using this ground mesh

.. figure:: /images/tutorial/02/08.jpg
   :align: center
   
For the live preview to work, make sure the "Realtime Update" button is enabled in the Theme Editor

.. figure:: /images/tutorial/02/09.jpg
   :align: center

Another criteria for the live preview to work is that a dungeon in the scene should reference the theme that is currently being edited in the theme editor

Add More Prefabs
^^^^^^^^^^^^^^^^

Go ahead and add prefabs under the following markers: **Wall**, **Fence** and **Door**

.. figure:: /images/tutorial/02/10.jpg
   :align: center


.. figure:: /images/tutorial/02/11.jpg
   :align: center


Add Wall Pillars
^^^^^^^^^^^^^^^^

Drag drop the ``Pillar2`` prefab to the theme editor and link it to the ``WallSeparator`` marker node

.. figure:: /images/tutorial/02/12.jpg
   :align: center

We'll need to make this pillar a bit bigger. Select the node you just dropped and modify the Scale parameter under Offset category

.. figure:: /images/tutorial/02/13.jpg
   :align: center

.. figure:: /images/tutorial/02/14.jpg
   :align: center


Add Windows
^^^^^^^^^^^
We have two wall meshes in the samples folder

.. figure:: /images/tutorial/02/15.jpg
   :align: center

The other one (``Wall2``) has a window. Lets configure the theme to sometimes use this second mesh so we have windows

Drag drop ``Wall2`` prefab on to the theme editor and place it **before** (left of) the existing wall prefab node

.. figure:: /images/tutorial/02/16.jpg
   :align: center


When you connect this to the ``Wall`` marker node, you'll notice it has picked up the window node for all the walls

.. figure:: /images/tutorial/02/17.jpg
   :align: center


This is because Dungeon Architect starts executing the nodes from left to right. When the condition was satisfied to pick the first node, it stopped execution and never came to the second node. 

There are multiple ways you can control this condition, the simplest being adjusting the probablity of selection.

Select the node you just dropped and change the probability to ``0.5`` (this would mean it gets selected 50% of the time).  The other 50% of the time, it would not be selected and the execution would then move to the next node, and hence selecting the non-windowed wall node

.. figure:: /images/tutorial/02/18.png
   :align: center

.. figure:: /images/tutorial/02/19.jpg
   :align: center
   
   Half the walls have windows


Add Wall Decorations
^^^^^^^^^^^^^^^^^^^^

There's a photo frame prefab we'd like to attach to every wall

.. figure:: /images/tutorial/02/20.jpg
   :align: center
   
Drag drop this prefab to the theme editor **before** the two existing nodes and link it to the ``Wall`` marker node

.. figure:: /images/tutorial/02/21.jpg
   :align: center


This will cause all the walls to disappear and be replaced with this photo frame

.. figure:: /images/tutorial/02/22.jpg
   :align: center

This is because once the photo frame was selected, the execution stopped and the the wall nodes further down the line were not executed.    

Selected the photo frame and uncheck the flag "Consume on Attach".  This will cause the execution to continue further even though this node was selected by the theming engine


.. figure:: /images/tutorial/02/23.jpg
   :align: center
   

Lets adjust the offset of the photo frame (position and rotation) to make it properly align with the inner walls

Select the photo frame node and change the position to ``(0, 2, -0.22)`` and rotation to ``(0, 180, 0)``

.. figure:: /images/tutorial/02/24.png
   :align: center
   

The photo frame is aligned with the walls

.. figure:: /images/tutorial/02/25.jpg
   :align: center


Marker Emitters
^^^^^^^^^^^^^^^

We have an issue with the photo frames. They also spawn near windows

.. figure:: /images/tutorial/02/26.jpg
   :align: center


``Marker Emitters`` allow you to emit marker names from any of your dropped prefab nodes.  This means, we can define a new marker node (e.g. ``MyWallDeco``) and then emit that marker from the wall node that doesn't have a window (``Wall1`` prefab).  All our wall decorations can now go under this ``MyWallDeco`` marker and it will show up only near solid walls


Right click on an empty area in the theme editor and select ``Add Marker Node``

.. figure:: /images/tutorial/02/27.png
   :align: center


Select the node and change its name to ``MyWallDeco``


.. figure:: /images/tutorial/02/28.png
   :align: center


Break the link to the photo frame

.. figure:: /images/tutorial/02/29.png
   :align: center


Connect this under ``MyWallDeco`` marker node.  All the future wall decorations can also go under this marker

.. figure:: /images/tutorial/02/30.png
   :align: center


Now emit this marker from the wall node that doesn't contain a window

Drag a link out of the bottom of the solid wall prefab node and release the mouse in an empty area


.. figure:: /images/tutorial/02/31.png
   :align: center


.. figure:: /images/tutorial/02/32.png
   :align: center


You can follow the same method to create another type of decoration (e.g. MyWindowDeco) and emit it from under the windowed wall node. In this example, I've added a flower pot in the windows

.. figure:: /images/tutorial/02/33.jpg
   :align: center

Align with Offset
^^^^^^^^^^^^^^^^^

Dungeon Architect can adapt to any modular asset regardless of the prefab pivot position.  If the pivots are off, you can always adjust them from the Offset section of the node's properties

Sometimes, it is difficult to line up the ground node, as there is no point of reference to compare with. 

In that case, turn on Debug Draw and build the dungeon. 

.. figure:: /images/tutorial/02/34.png
   :align: center


.. figure:: /images/tutorial/02/35.jpg
   :align: center

This ground asset has its pivot on the corner instead of the center.   We'll add an offset of position ``(-2, 0, -2)`` to fix it and align with the debug drawn boundaries

.. figure:: /images/tutorial/02/36.jpg
   :align: center


It is important to first align the ground mesh and then use that as a reference to align your walls and fences.  If the ground is not aligned correctly, the rest will also not align (since you will be using an incorrect point of reference for aligning the rest)

Recap
^^^^^
In this section we learnt the following:

* *Probablity* - Controls the percentage chance of a node being selected.  A value of 1 means 100% selection chance. A value of 0.25 means 25% selection chance
* *Execution Order* - The theme engine executes all the nodes under a marker node from left to right. If it selects a certain node, it stops executing, unless the ``Consume on Attach`` flag is unchecked
* *Marker Emitters* - You can create complex hierarchies with your own marker nodes, giving you more freedom to decorate your dungeons
 
 





