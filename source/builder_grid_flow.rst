Grid Flow Builder
=================

The Grid Flow Builder offers a rich set of tools to control the flow of your dungeons and item placement


Create a Grid Flow Dungeon
--------------------------

Setup Dungeon Actor
^^^^^^^^^^^^^^^^^^^

Create a new Level and drop in a dungeon actor

.. image:: /images/tutorial/A/02.jpg
   :align: center
   

Inspect the properties of the dungeon actor you just dropped.   Set the `Builder Class` to ``GridFlowBuilder``

.. image:: /images/tutorial/E/01.png
   :align: center
   

Setup Theme
^^^^^^^^^^^

Click the ``+`` icon next to the Themes array to create a new theme entry.  

.. image:: /images/tutorial/E/02A.png
   :align: center

Here we'll assign an existing theme from the samples folder.  For this, we'll need to enable `Show Plugin Content` from the view options

.. image:: /images/tutorial/E/02B.png
   :align: center

.. image:: /images/tutorial/E/02C.png
   :align: center


We'll assign the theme ``T_DefaultGridFlow``.   

.. image:: /images/tutorial/E/03.png
   :align: center


.. note::
	The above theme theme file is under `Dungeon Architect Content > Builders > GridFlowContent > Theme` folder

	.. image:: /images/tutorial/E/04.png
	   :align: center


Setup GridFlow Graph
^^^^^^^^^^^^^^^^^^^^

This builder requires another asset called the `Grid Flow Graph`.   This is a graph that helps you  control the flow of your dungeon. In this section, we'll use an existing graph from the samples folder

Select the Dungeon actor and in the `Grid Flow` setting assign the following asset ``DefaultGridFlow``.  This is in the folder `Dungeon Architect Content > Builders > GridFlowContent > FlowGraph`

.. image:: /images/tutorial/E/05.png
   :align: center

.. image:: /images/tutorial/E/06.png
   :align: center

.. image:: /images/tutorial/E/07.png
   :align: center

Build Dungeon
^^^^^^^^^^^^^

Select the Dungeon actor and click `Build Dungeon` button from the Details panel

.. figure:: /images/tutorial/E/09.jpg
   :align: center
   
   GridFlow dungeon built using the Prehistoric theme

.. figure:: /images/tutorial/E/08.jpg
   :align: center
   
   GridFlow dungeons support key-locks
   

Grid Flow Editor
----------------

Let's open the GridFlow asset in the editor:

Navigate to ``Dungeon Architect Content > Builders > GridFlowContent > FlowGraph`` and double click on ``DefaultGridFlow``

This will open the `Grid Flow Editor`

.. figure:: /images/tutorial/E/10.jpg
   :align: center
   
   Grid Flow Editor
   
Click the Build button toolbar to build the graph

.. image:: /images/tutorial/E/11.png
   :align: center

.. image:: /images/tutorial/E/12.jpg
   :align: center


Keep hitting build to get a new dungeon

.. image:: /images/tutorial/E/13.gif
   :align: center


Explore Grid Flow Graph
^^^^^^^^^^^^^^^^^^^^^^^

After you've built a dungeon in the editor (by hitting the `Build` button on the toolbar), you can select each node in the execution graph and see how the dungeon layout was built, as shown in the lower preview panels

.. figure:: /images/tutorial/E/15.gif
   :align: center

   Select an execution graph node to preview the build process



Editor Panels
-------------

The Grid Flow Editor has the following panels

Execution Graph Panel
^^^^^^^^^^^^^^^^^^^^^

This is where you design the flow of your dungeon. All other panels are for previewing the result of this panel

.. image:: /images/tutorial/E/14A.jpg
   :align: center


Layout Graph Panel
^^^^^^^^^^^^^^^^^^

The initial level is designed in a higher level layout graph

.. image:: /images/tutorial/E/14B.jpg
   :align: center


Tilemap Panel
^^^^^^^^^^^^^

The result of the layout graph is eventually transferred over to a tilemap. The resulting tilemap is previewed here

.. image:: /images/tutorial/E/14C.jpg
   :align: center

Preview Viewport Panel
^^^^^^^^^^^^^^^^^^^^^^

The 3D representation of the final Dungeon

.. image:: /images/tutorial/E/14D.jpg
   :align: center


Design a GridFlow Graph
-----------------------

In the previous section, we used an existing Grid Flow graph from the samples folder. In this section, we'll design one ourselves.

Setup
^^^^^

Close the Grid Flow Editor, if open

Right click on the `Content Browser` and choose Dungeon Architect > Grid Flow.  This will create a new Grid Flow asset. Rename it to something appropriate and double click to open it in the `Grid Flow Editor`

.. image:: /images/tutorial/E/18.png
   :align: center

.. image:: /images/tutorial/E/17.jpg
   :align: center

Notice that there is only one node in the Execution graph, the ``Result`` node.   Our final output should be connected to this node


Create Grid
^^^^^^^^^^^

Right click on an empty area in the Execution Graph and from the context menu select ``Layout Graph > Create Grid``

.. figure:: /images/tutorial/04/menu/L_CreateGrid.png
   :align: center


.. figure:: /images/tutorial/04/21.png
   :align: center
   

Connect this node to the ``Result`` node and hit play 


   
.. figure:: /images/tutorial/04/22.png
   :align: center

   
.. figure:: /images/tutorial/04/11.png
   :align: center
   

This node creates an initial grid to work with 

.. figure:: /images/tutorial/04/23.png
   :align: center


In this builder, you first design your level in an abstract layout graph like this and then move the final result to a tilemap


Create Main Path
^^^^^^^^^^^^^^^^

We'll next create a main path within this grid. The main path has a spawn point and goal

Create a new node ``Layout Graph > Create Math Path``

.. figure:: /images/tutorial/04/menu/L_CreateMainPath.png
   :align: center
   


Unlink the ``Create Grid`` node from the ``Result`` node (do this by right clicking on the node's orange border)


.. figure:: /images/tutorial/04/24.png
   :align: center


Link the nodes up like below and hit Play

.. figure:: /images/tutorial/04/25.png
   :align: center


This node creates a main path in the grid.  Keep hitting the play button for different result

.. figure:: /images/tutorial/04/26.gif
   :align: center
   
.. note::
   If you do not see random results when you hit play, make sure randomize is enabled.  Enable this by clicking on an empty area in the Execution Graph to show the properties. In the inspector, select ``Randomize Seed``


Select the ``Create Main Path`` node and inspect the properties

.. figure:: /images/tutorial/04/27.png
   :align: center

We'll leave everything to default for now

Notice the `Path Name` parameter is set to ``main``   This is the name of the path and we will be referencing this path in the future nodes with this name

You can adjust the size of the path.   ``Start Marker Name`` and ``Goal Marker Name`` lets you specify a name for the markers. You can then create these markers in the theme file and add any object you like.    In the `Prehistoric` theme, there's a marker already created with these names and a player controller is placed under ``SpawnPoint`` marker and a level goal handler prefab is placed under ``LevelGoal`` marker

.. figure:: /images/tutorial/04/28.jpg
   :align: center


Create Alternate Path
^^^^^^^^^^^^^^^^^^^^^

We'll next create an alternate path pathing off the main path so the player has another way of reaching the goal

Create a new node ``Layout Graph > Create Path``

.. figure:: /images/tutorial/04/menu/L_CreatePath.png
   :align: center

Connect the nodes together like below

.. figure:: /images/tutorial/04/29.png
   :align: center

Leave all the properties as default and hit play

.. figure:: /images/tutorial/04/30.png
   :align: center


Select the ``Create Path`` node and inspect the properties

.. figure:: /images/tutorial/04/31.png
   :align: center


Change the `Path Name` from ``path`` to ``alt``.  We will be referencing this path as ``alt`` in the future

.. figure:: /images/tutorial/04/32.png
   :align: center


You can specify the paths from which this path should start and end.    The `Start From Path` parameter is set to ``main``, referencing the main path we created in the previous section

The `End On Path` is left empty, so the end of this path doesn't connect back to anything.   We'd like this path to connect back to the main path. 

Set the `End On Path` parameter to ``main``

.. figure:: /images/tutorial/04/33.png
   :align: center


======================= =======================
**Min Path Size**       3
**Max Path Size**       3
**Path Name**           alt
**Node Color**          orange
**Start From Path**     main
**End On Path**         main
======================= =======================

This will make the alternate path (orange) connect back to the main path (green)

.. figure:: /images/tutorial/04/34.png
   :align: center


Keep hitting Play for different results

.. figure:: /images/tutorial/04/35.gif
   :align: center


Create Treasure Room (Main)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

We'll add a treasure room connected to the main path

Add a new node ``Layout Graph > Create Path`` and set it up as follows:

.. figure:: /images/tutorial/04/37.png
   :align: center

.. figure:: /images/tutorial/04/36.png
   :align: center

======================= =======================
**Min Path Size**       1
**Max Path Size**       3
**Path Name**           treasure_main
**Node Color**          yellow
**Start From Path**     main
**End On Path**         main
======================= =======================

.. figure:: /images/tutorial/04/38.png
   :align: center


Create Treasure Room (Alt)
^^^^^^^^^^^^^^^^^^^^^^^^^^

We'll add another treasure room connected to the ``alt`` path but keep the ``End On Path`` parameter empty so it doesn't connect back to anything:

Add a new node ``Layout Graph > Create Path`` and set it up as follows:

.. figure:: /images/tutorial/04/39.png
   :align: center

.. figure:: /images/tutorial/04/40.png
   :align: center

======================= =======================
**Min Path Size**       1
**Max Path Size**       1
**Path Name**           treasure_alt
**Node Color**          yellow
**Start From Path**     alt
**End On Path**         
======================= =======================

.. figure:: /images/tutorial/04/41.png
   :align: center


Create Key Room
^^^^^^^^^^^^^^^

We'll create a room connected to the main path which will act as the key room. We'll later configure this room to have a key that opens up a lock in the main path. It will also have a NPC (key guardian) guarding the key

Add a new node ``Layout Graph > Create Path`` and set it up as follows:


.. figure:: /images/tutorial/04/42.png
   :align: center

.. figure:: /images/tutorial/04/43.png
   :align: center

======================= =======================
**Min Path Size**       1
**Max Path Size**       1
**Path Name**           key_room
**Node Color**          cyan
**Start From Path**     main
**End On Path**         
======================= =======================

.. figure:: /images/tutorial/04/44.png
   :align: center

.. note:: We've named this path ``key_room``. It will be referenced later on when creating the key locks


Create Key-Lock (Main)
^^^^^^^^^^^^^^^^^^^^^^

We'll next create a key-lock system on the main path.  Our key will go on the Key Room we created earlier (``key_room`` path) and the lock will be somewhere in the main branch (``main`` path)


Add a new node ``Layout Graph > Create Key Lock`` and set it up as follows:

.. figure:: /images/tutorial/04/menu/L_CreateKeyLock.png
   :align: center
   
.. figure:: /images/tutorial/04/45.png
   :align: center

.. figure:: /images/tutorial/04/46.png
   :align: center

======================= =======================
**Key Branch**          key_room
**Lock Branch**         main
**Key Marker Name**     KeyMain
**Lock Marker Name**    LockMain
======================= =======================

.. figure:: /images/tutorial/04/47.png
   :align: center


Specify the `Key Branch` as ``key_room`` and `Lock Branch` as ``main``

Set marker name for the key as ``KeyMain`` and lock as ``LockMain``.    Then in the theme file, you'd create marker nodes with these names and add your key and locked gate prefabs.   

The prehistoric theme already has these setup

.. figure:: /images/tutorial/04/48.png
   :align: center
   

Create Key-Lock (Treasure Main)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We need a key-lock to guard the treasure room in the main branch

Add a new node ``Layout Graph > Create Key Lock`` and set it up as follows:


.. figure:: /images/tutorial/04/49.png
   :align: center

.. figure:: /images/tutorial/04/50.png
   :align: center

======================= =======================
**Key Branch**          main
**Lock Branch**         treasure_main
**Key Marker Name**     KeyTreasure
**Lock Marker Name**    LockTreasure
======================= =======================


.. figure:: /images/tutorial/04/51.png
   :align: center


Set marker name for the key as ``KeyTreasure`` and lock as ``LockTreasure``.    Then in the theme file, you'd create marker nodes with these names and add your key and locked gate prefabs.   

The prehistoric theme already has these setup

.. figure:: /images/tutorial/04/52.png
   :align: center
   
   
Spawn Enemies (Main, Alt)
^^^^^^^^^^^^^^^^^^^^^^^^^

We'll use the ``Spawn Items`` node to spawn enemies on the ``main`` and ``alt`` paths

Create a new node ``Layout Graph > Spawn Items`` and set it up as follows:


.. figure:: /images/tutorial/04/menu/L_SpawnItems.png
   :align: center
   
.. figure:: /images/tutorial/04/53.png
   :align: center

.. figure:: /images/tutorial/04/54.png
   :align: center

======================= =======================
**Paths**               main, alt
**Item Type**           Enemy
**Marker Name**         Grunt
**Min Count**           1
**Max Count**           5
======================= =======================

.. figure:: /images/tutorial/04/55.png
   :align: center


This will spawn enemies in the nodes, gradually increasing the number of enemies based on the difficulty. The difficulty increases as we get closer to the goal. You can control this from the `Spawn Method` properties. Leave it to default for now


We've specified the marker name as ``Grunt`` and an appropriate marker node should be created in the theme file so we can spawn prefabs under it.  The pre-historic theme already has this marker


.. figure:: /images/tutorial/04/56.png
   :align: center


You can control the placement of items (in the tilemap) from the `Placement Method` property section. Leave it to default for now

Spawn Bonus (Treasure Chests)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Spawn treasure chests in your bonus rooms using the `Spawn Items` node


Create a new node ``Layout Graph > Spawn Items`` and set it up as follows:


.. figure:: /images/tutorial/04/57.png
   :align: center

.. figure:: /images/tutorial/04/58.png
   :align: center

========================= =======================
**Paths**                 treasure_main, treasure_alt
**Item Type**             Bonus
**Marker Name**           Treasure
**Min Count**             1
**Max Count**             1
**Min Spawn Difficulty**  1
========================= =======================

.. figure:: /images/tutorial/04/59.png
   :align: center
   

We've specified the marker name as ``Treasure`` and an appropriate marker node should be created in the theme file so we can spawn prefabs the treasure chest under it.  The pre-historic theme already has this marker

.. figure:: /images/tutorial/04/60.png
   :align: center
   

The `Min Spawn Difficulty` is set to ``1``.   The first node in the branch will have a difficulty of ``0`` and the last node ``1``.  Sometimes, the yellow branch may be 3 nodes long.  Since we want the chest to occur only on the last node, we've set this value to ``1``

Spawn Key Guardian
^^^^^^^^^^^^^^^^^^

We'll add an NPC in the Key room guarding the key

Create a new node ``Layout Graph > Spawn Items`` and set it up as follows:



.. figure:: /images/tutorial/04/61.png
   :align: center

.. figure:: /images/tutorial/04/62.png
   :align: center

========================= =======================
**Paths**                 key_room
**Item Type**             Enemy
**Marker Name**           KeyGuardian
**Min Count**             1
**Max Count**             1
========================= =======================

.. figure:: /images/tutorial/04/63.png
   :align: center
   
You'll need to create a marker named ``KeyGuardian`` in the theme file and place your NPC prefab under it.   This marker doesn't exist in the `Prehistoric` theme and you'll need to create it yourself if you want to visualize it


Spawn Health Pack
^^^^^^^^^^^^^^^^^

We'll use the `Spawn Items` node to spawn a few health pickups along the `main` and `alt` paths

This section also shows you how to use the `Custom` Item Type 

Create a new node ``Layout Graph > Spawn Items`` and set it up as follows:



.. figure:: /images/tutorial/04/64.png
   :align: center

.. figure:: /images/tutorial/04/65.png
   :align: center

========================= =======================
**Paths**                 main, alt
**Item Type**             Custom
**Marker Name**           HealthPickup
**Min Count**             0
**Max Count**             1
**Spawn Probability**     0.5 

**Custom Item Info**
-------------------------------------------------
>> **Item Type**          health_pickup
>> **Text**               Health
>> **Text Color**         [Red]
>> **Background Color**   [White]
========================= =======================

.. figure:: /images/tutorial/04/66.png
   :align: center
   
   
.. note:: You'll need to create a marker named ``HealthPickup`` in your theme file and add your health pack prefab



Finalize Layout Graph
^^^^^^^^^^^^^^^^^^^^^

After we are done designing the layout graph, we'll need to finalize it with the `Finalize Graph` node.    This node does a few things:

* Move the locks from the nodes on to the links
* Create one way doors (so we don't go around locked doors)
* Assign room types (Room, Corridor, Cave)

Create a new node ``Layout Graph > Finalize Graph`` and set it up as follows:

.. figure:: /images/tutorial/04/menu/L_Finalize.png
   :align: center

.. figure:: /images/tutorial/04/67.png
   :align: center

Leave all the properties to default

.. figure:: /images/tutorial/04/68.png
   :align: center


.. figure:: /images/tutorial/04/69.gif
   :align: center


We are now ready to create a tilemap from this



Initialize Tilemap
^^^^^^^^^^^^^^^^^^

Create a new node ``Tilemap > Initialize Tilemap`` and set it up as follows:

.. figure:: /images/tutorial/04/menu/T_Initialize.png
   :align: center
   
   
.. figure:: /images/tutorial/04/70.png
   :align: center


.. figure:: /images/tutorial/04/71.png
   :align: center


.. figure:: /images/tutorial/04/72.png
   :align: center


You can control the thickness of the caves from the `Cave Thickness` parameter.   Each node on the layout graph gets converted into rooms in the tilemap.  

The parameter `Tilemap Size Per Node` controls how many tiles are used to generate a room from the node. Bump this number up if you want more space in your rooms

If you want a more uniform grid like look on your rooms, bring the `Perturb Amount` close to ``0``

`Layout Padding` adds extra tiles around the dungeon layout.   Set to ``5`` so we can apply some decorations outside the dungeon bounds

When you select a node on the layout graph, the tiles that belong to the node light up.  This is controlled by the `Color Settings` parameters


Add Background Elevation
^^^^^^^^^^^^^^^^^^^^^^^^

We are going to create overlays and merge them with the original tilemap.   Create the following two nodes:

* Create a node ``Tilemap > Create Tilemap Elevations``
* Create a node ``Tilemap > Merge Tilemaps``

.. figure:: /images/tutorial/04/menu/T_CreateElevation.png
   :align: center
   
.. figure:: /images/tutorial/04/menu/T_Merge.png
   :align: center


Link them up like below:

.. figure:: /images/tutorial/04/73.png
   :align: center
   
.. figure:: /images/tutorial/04/74.png
   :align: center
   
   Create Tilemap Elevation properties
   
Update the properties

========================= =======================
**Noise Frequency**       0.1
**Num Steps**             8
**Min Height**            0.5
**Max Height**            3.5
**Sea Level**             -1
========================= =======================


.. figure:: /images/tutorial/04/75.png
   :align: center
   
   Create Tilemap Elevation Node Result


We've specified the marker name as ``Rock``.   If you place objects under the specified marker node in the theme editor, they will show up on these tiles at the given height

.. note:: The Min/Max height is logical and will be mulitplied by the dungeon config's Grid Size Y value.  If the GridSize is ``(4, 2, 4)`` in the DungeonGridFlow game object's config and the tile height happens to be ``2.5``, the actual placement will be on ``2.5 * 2 = 5``


Add Tree Overlays
^^^^^^^^^^^^^^^^^

We'll overlay trees on our dungeon using a noise parameter. These overlays will be placed such that they will not block the main path

Create a node ``Tilemap > Create Tilemap Overlay``

.. figure:: /images/tutorial/04/menu/T_CreateOverlay.png
   :align: center


.. figure:: /images/tutorial/04/76.png
   :align: center
   
   Create Tilemap Overlay Node Connection
   
.. figure:: /images/tutorial/04/77.png
   :align: center
   
   Create Tilemap Overlay Node properties
   

============================= =======================
**Noise Settings**
-----------------------------------------------------
**> Noise Frequency**         0.2
**> Noise Max Value**         1.5
**> Noise Threshold**         0.75
**> Min Dist From Main Path** 1

**Merge Config**
-----------------------------------------------------
**> Max Height**              1
============================= =======================
   
.. figure:: /images/tutorial/04/78.png
   :align: center
   
   Result of the Create Tilemap Overlay Node
   
.. figure:: /images/tutorial/04/79.png
   :align: center
   
   Merged result
   
   
Finalize Tilemap
^^^^^^^^^^^^^^^^

Finalize the tilemap to complete the grid flow graph

Create a node ``Tilemap > Finalize Tilemap``

.. figure:: /images/tutorial/04/menu/T_Finalize.png
   :align: center
   

.. figure:: /images/tutorial/04/80.png
   :align: center
   
   
.. figure:: /images/tutorial/04/81.png
   :align: center
   
Finalize Tilemap node places all the items on to the tilemap (enemies, keys, bonus etc)


Build Dungeon
^^^^^^^^^^^^^

Assign this grid flow graph to your DungeonGridFlow game object and click `Build Dungeon`


.. figure:: /images/tutorial/04/82.png
   :align: center
   
   
.. figure:: /images/tutorial/04/83.jpg
   :align: center
   


Optimize Tilemap
^^^^^^^^^^^^^^^^
   
When the tilemap based level is generated, there are many tiles that the player might never see, as they are far away from the dungeon layout

.. figure:: /images/tutorial/04/84.jpg
   :align: center
   

The `Optimize Tilemap` removes tiles that are away from the specified distance from the dungeon layout bounds
   
   
.. figure:: /images/tutorial/04/86.png
   :align: center
   
   Optimize Tilemap Node Result

   
.. figure:: /images/tutorial/04/87.gif
   :align: center

   Optimize Tilemap Before / After
   
   
   
Create a node ``Tilemap > Optimize Tilemap``

.. figure:: /images/tutorial/04/menu/T_Optimize.png
   :align: center
   
Connect it before the `Finalize Tilemap` node like below:

.. figure:: /images/tutorial/04/88.png
   :align: center
   
   
.. figure:: /images/tutorial/04/89.png
   :align: center
   
   Optimize Tilemap Node properties


Rebuild the dungeon in the scene view

.. figure:: /images/tutorial/04/85.gif
   :align: center

   Optimize Tilemap Before / After
  


Key Lock System
---------------

The spawned Key and Lock game objects will have the following components attached to it by Dungeon Architect


.. figure:: /images/tutorial/04/90.jpg
   :align: center
   
   New Components attached to the Key Prefab


.. figure:: /images/tutorial/04/91.jpg
   :align: center
   
   New Components attached to the Locked Door Prefab


Key Component
^^^^^^^^^^^^^

The builder will attach a new component ``GridFlowDoorKeyComponent`` to the spawned key prefab

.. figure:: /images/tutorial/04/92.png
   :align: center


This component contains the KeyId and a reference to all the locks that this key can open

==================== =============================================
**Key Id**           The Key Id
**Valid Lock Ids**   List of Lock Ids that can be opened by this key
**Lock Refs**        References to the spawned lock game objects that can be opened by this key
==================== =============================================

Lock Component
^^^^^^^^^^^^^^

The builder will attach a new component ``GridFlowDoorLockComponent`` to the spawned lock prefab

.. figure:: /images/tutorial/04/93.png
   :align: center

This component contains the LockId and a reference to all the keys that open this lock

==================== =============================================
**Lock Id**          The Lock Id
**Valid Key Ids**    List of Key Ids that open this lock
**Valid Key Refs**   References to the spawned key game objects that open this lock
==================== =============================================


Sample
^^^^^^

Game Sample Scene: ``Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Scenes/GridFlowBuilderDemo_Game``

The GridFlow game sample contains a working example of how you can implement a key lock system. There are many ways of implementing this, this sample shows one such way. 

The Sample has the following scripts:

* Inventory: Saves the picked up keys in the inventory
* LockedDoor: A script that implements the door opening logic. This script is added to the locked door prefab. When something collides with the door trigger, it checks if it has an inventory.  If it does, it checks if the inventory contains any of the valid keys that can open this door


LockedDoor script location: ``Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Scripts/DemoGame/Door/LockedDoor.cs`` 

.. code-block:: c#

	bool CanOpenDoor(Collider other)
	{
		var inventory = other.gameObject.GetComponentInChildren<Inventory>();
		if (inventory != null)
		{
			// Check if any of the valid keys are present in the inventory of the collided object
			foreach (var validKey in validKeys)
			{
				if (inventory.ContainsItem(validKey))
				{
					return true;
				}
			}
		}
		return false;
	}




Mini-Map
--------

Display a 2D minimap with fog of war 

.. figure:: /images/tutorial/04/94.jpg
   :align: center
   

The ``DungeonGridFlow`` prefab already comes pre-configured with the minimap.  This is done with the ``GridFlowMinimap`` component: 

.. figure:: /images/tutorial/04/95.png
   :align: center
   

======================== =====================================
**Update Frequency**     Control the frequency of minimap updates. The updates can run at a lower fps for better performance
**Enable Fog of War**    Hides parts of the map that is not explored yet
**See Through Walls**    If this is disabled, unexplored area behind a wall will not be made visible.  This works if Fog of War is enabled
**Minimap Texture**      The Render Target texture that the minimap will be rendered on 
**Icons**                The icons to overlay on special tiles

**Init Mode**            
--------------------------------------------------------------
 >> On Dungeon Rebuild   The minimap layout texture is regenerated when the dungeon rebuilds
 >> On Play              The minimap layout texture is generated when you start play
 >> Manual               The minimap layout texture is generated only when you manually build it from script
======================== =====================================


Setup
^^^^^

The minimap requires you to provide a Render Texture asset in the `Minimap Texture` property.  The minimap will be rendered in this texture.  You can then apply this texture anywhere (in your UI elements, in a mesh etc)

Create a new Render Texture asset. Use the Create menu in the Project window: ``Create > Render Texture``

.. figure:: /images/tutorial/04/96.png
   :align: center


Select the Render Texture asset and inspect the properties

.. figure:: /images/tutorial/04/97.png
   :align: center


Change the following:

======================== =====================================
**Size**                 Change to 512x512 (or the quality you are comfortable with)
**Depth Buffer**         No Depth buffer (we don't need it here)
**Filter Mode**          Point (so we get sharp tile edges instead of a blurry image)
======================== =====================================


Assign this `Render Texture` asset to your DungeonGridFlow game object's minimap component

.. figure:: /images/tutorial/04/98.jpg
   :align: center


Dungeon Architect will automatically update this texture based on the specified `Update Frequency`. You can assign this texture anywhere on your UI. You can also attach it on a mesh

Show in UI
^^^^^^^^^^

Open the game sample scene: ``Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Scenes/GridFlowBuilderDemo_Game``

There's a UI canvas in the hierarchy. Expand and inspect it:


.. figure:: /images/tutorial/04/99.png
   :align: center


There is a `RawImage` Canvas Item in there. It was created like this:

.. figure:: /images/tutorial/04/102.jpg
   :align: center


Select the RawImage item and configure it like this:

.. figure:: /images/tutorial/04/101.png
   :align: center

.. figure:: /images/tutorial/04/100.jpg
   :align: center

The Render Texture was assigned there so it will show our minimap


Add to a Material
^^^^^^^^^^^^^^^^^

While playing the sample game, if you look down, you notice the player holding a map in the hand (like in Minecraft).   This map shows the minimap in realtime

.. figure:: /images/tutorial/04/103.jpg
   :align: center


The texture was simply added to an unlit material, and the material was then applied to that mesh

Create a Material as below:

.. figure:: /images/tutorial/04/104.png
   :align: center

* Set the Shader to ``UI/Unlit/Transparent``
* Set the texture to your Render Texture asset

You can now apply this material anywhere (e.g. in a large billboard in your world, a small map that the player holds,  dashboard of a vehicle etc)


.. seealso::
	Check the sample game to see how this was done

	================== ===========================
	**Tablet Prefab**  `Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Art/Prefab/Tablet_Map`
	**Material**       `Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Art/Materials/Mat_TabletScreen`
	================== ===========================


Minimap Tracked Objects
^^^^^^^^^^^^^^^^^^^^^^^

The minimap can track any object in the scene.  You do this by adding the `GridFlowMinimapTrackedObject` component to the desired prefab

.. figure:: /images/tutorial/04/105.png
   :align: center
   
   Added to the Player prefab
   
   
.. figure:: /images/tutorial/04/106.png
   :align: center
   
   Added to the Enemy prefab


It has the following features:

* The tracked object can explore the minimap (e.g. player and allies)
* Specify an icon, color and scale of the object in the minimap
* the icon can rotate to indicate the game object's Y rotation (good for player game objects)


You'd want to turn on `Explores Fog of War` only for the player and other relavant objects.   The icon can be greyscale and you can apply a tint on it with different colors (e.g. on key icon but different colors applied to the red key prefab, blue key prefab and so on)

.. seealso::
	Check the sample game prefabs to see how the component was configured

	==================== ====================
	Player Controller    Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Scenes/DemoGameSupportFiles/Prefabs/GridFlowPlayerController
	Grund NPC            Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Scenes/DemoGameSupportFiles/Prefabs/Enemy
	Key (Red)            Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Art/Prefab/KeySkull_Red
	Key (Blue)           Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Art/Prefab/KeySkull_Blue
	Door (Yellow)        Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Art/Prefab/DoorLargeLocked_Yellow
	Door (Green)         Assets/DungeonArchitect_Samples/DemoBuilder_GridFlow/Art/Prefab/DoorLargeLocked_Green
	==================== ====================

