Advanced Dungeons
=================
Marker Emitters
---------------

Marker Emitters are blueprint scripts (or C++) that lets you emit your own markers anywhere in the map


.. figure:: /images/tutorial/H/da_design_me.png
   :align: center

   Architecture

As seen previously, *Markers* are emitted by the Dungeon Builder class around the layout of the dungeon (e.g. Wall, Ground, Fence etc) and you can insert actors at that location from the Theme graph.  You can even create your own markers emitted off of those parent markers, but without *Marker Emitters* you are restricted to the starting markers the dungeon builder has initially emitted for you

Marker Emitters gives you a lot of flexibility and you can query the dungeon model and emit markers anywhere in the map

A Marker Emitter is invoked right after the Dungeon Builder emits all the markers for the dungeon (Ground, Wall etc)

Creating a Marker Emitter
^^^^^^^^^^^^^^^^^^^^^^^^^

Create a new Blueprint class derived from DungeonMarkerEmitter

.. figure:: /images/tutorial/H/create_marker_emiter_dialog.png
   :align: center

   Create a new marker emitter

Assign the created blueprint marker emitter to the Dungeon Actor


.. figure:: /images/tutorial/H/assign_marker_emitter.png
   :align: center

   Assign to the Dungeon actor

Start placing your logic in the blueprint by overriding the **Emit Markers** function


.. figure:: /images/tutorial/H/marker_emitter_04.png
   :align: center

   Override the EmitMarkers function

This method is invoked by the engine and lets you emit as many markers as you like into the scene with any transforms.

To emit a marker, create a *Emit Marker* node


.. figure:: /images/tutorial/H/marker_emitter_05.png
   :align: center

   Emit Marker Node

You can emit as many markers as you like

Theme Preview
^^^^^^^^^^^^^

If you want to preview your marker emitter logic in the Theme Editor's 3D Preview viewport,  you can set it up like this:

Navigate to the theme editor's 3D Viewport > Properties > Dungeon


.. figure:: /images/tutorial/H/marker_emitter_te_1.png
   :align: center 

   Theme Editor's 3D Viewport > Properties > Dungeon

This will open up the dungeon properties. Add your marker emitter there and the preview viewport will pick up the markers emitted by your Marker Emitter blueprint script and show it in the preview viewport


.. figure:: /images/tutorial/H/marker_emitter_te_2.jpg
   :align: center

   Theme Editor's 3D Viewport > Properties > Dungeon


Example #1
^^^^^^^^^^

This marker emitter queries the dungeon model and emits a marker at the center of all the rooms


.. figure:: /images/tutorial/H/marker_emitter_eg1_1.png
   :align: center

   Sample Marker Emitter


.. figure:: /images/tutorial/H/marker_emitter_eg1_2.png
   :align: center

   Marker Emitted with this name


.. figure:: /images/tutorial/H/marker_emitter_eg1_3.png
   :align: center

   Create a Marker node with the same name


.. figure:: /images/tutorial/H/marker_emitter_eg1_4.png
   :align: center

   Theming engine picks it up and inserts it in the middle of the room

Example #2
^^^^^^^^^^

The *Hell Forge* demo has a good looking cave like system generated using Marker Emitters.

Since the rocks for the cave walls cannot be inserted in the Wall and Fence markers (as they are big and would block the passage), we need to find positions in the empty space that are further away from the walls and fences

This is done with a marker emitter blueprint `DA_InfinityBlade_Fire/Dungeons/Rules/MarkerEmitter/BPM_AdjacentCellEmitter`


.. figure:: /images/tutorial/H/marker_emitter_eg2_1.png
   :align: center

   Visualizing the emitter with different colored cubes


.. figure:: /images/tutorial/H/marker_emitter_eg2_2.jpg
   :align: center

   Visualizing the emitter with different colored cubes

The Hell Forge theme applies rocks to these markers (EmptySpaceN) and increases their scale as they move further away from the the ground


.. figure:: /images/tutorial/H/marker_emitter_eg2_3.jpg
   :align: center

   Theme to create Mountains using a Marker Emitter

This gives a nice progressive elevation to the mountains giving the impression that the pathways are naturally formed


.. figure:: /images/tutorial/H/marker_emitter_eg2_4.jpg
   :align: center

   Hell Forge theme with Mountains and Caves


Example #3
^^^^^^^^^^

Heres another example of a curved roof created over a room using marker emitters


.. figure:: /images/tutorial/H/marker_emitter_eg3_1.jpg
   :align: center

   

.. figure:: /images/tutorial/H/marker_emitter_eg3_2.jpg
   :align: center

   

.. figure:: /images/tutorial/H/marker_emitter_eg3_3.jpg
   :align: center

   





Query Interface
---------------

The query interface has various helper functions to query the structure of the dungeon.    You can use the query interface in your selector / transform logics or marker emitters for more control

Each builder implements its own query interface.    


Access the Query Interface
^^^^^^^^^^^^^^^^^^^^^^^^^^

You can access the query interface from different places



.. figure:: /images/tutorial/H/query_interface_access_selector_logic.png
   :align: center

   Query interface in the selection rule



.. figure:: /images/tutorial/H/query_interface_access_transform_logic.png
   :align: center

   Query interface in the transformer rule


.. figure:: /images/tutorial/H/query_interface_access_marker_emiter.png
   :align: center

   Query interface in the marker emitter


.. figure:: /images/tutorial/H/query_interface_access_dungeon_actor.png
   :align: center

   Query interface from other blueprints


Grid Query Interface
^^^^^^^^^^^^^^^^^^^^

The Grid Query Interface lets you query the structure of a grid builder based dungeon

Get Cells
#########

Gets a list of all the Cell IDs in the dungeon. A corridor patch or a room is a cell. A cell is always rectangular in shape, with a center and size


.. figure:: /images/tutorial/H/query_grid_GetCells.png
   :align: center

   Get Cells


Get Cells Of Type
#################

Similar to Get Cells function but filters the cells based on a type (Room, Coordor)


.. figure:: /images/tutorial/H/query_grid_GetCellsOfType.png
   :align: center

   Get Cells Of Type

Get Cell Dimension
##################

Gets the dimension of a cell.  This takes in a cell id and will return the center and the size of the cell


.. figure:: /images/tutorial/H/query_grid_GetCellDimension.png
   :align: center

   Get Cell Dimension

Get Path Between Cells
######################

Gets a valid path between any two cell points.  This can be used to create waypoints in your game.  There is an example in the quick start guide demonstrating this


.. figure:: /images/tutorial/H/query_grid_GetPathBetweenCells.png
   :align: center

   Get Path Between Cells


.. figure:: /images/tutorial/H/query_grid_path.jpg
   :align: center

   Query path between two cells


Get Furthest Rooms
##################

Find the furthest rooms in the dungeon.   This function returns two cell ID.  This can be useful for setting the start / end rooms (or spawn / boss rooms)


.. figure:: /images/tutorial/H/query_grid_GetFurthestRooms.png
   :align: center

   Get Furthest Rooms


Get Cell At Location
####################

Pass in a world location and get the cell id.  This is useful for finding the cell an actor is in.   For e.g., if you'd like to check if all NPCs in a room are dead before unlocking a door, you would iterate through all the actors and check if they are in the same room the player is in


.. figure:: /images/tutorial/H/query_grid_GetCellAtLocation.png
   :align: center

   Get Cell At Location


Get Cell Type
#############

Find the type of the cell (Room, corridor).    There is another category called CorridorPadding, which should also be considered a Corridor


.. figure:: /images/tutorial/H/query_grid_GetCellType.png
   :align: center

   Get Cell Type


Get Random Cell
###############

Gets a random cell from the dungeon.  

There also a version that takes in a random stream. You should use the random stream version if you want to guarantee the same dungeon for a particular configuration. The dungeon's random stream is access from within the selector and transform rules


.. figure:: /images/tutorial/H/query_grid_GetRandomCell.png
   :align: center

   Get Random Cell


Get Random Cell Of Type
#######################

Gets a random cell of a particular type from the dungeon.  

There also a version that takes in a random stream. You should use the random stream version if you want to guarantee the same dungeon for a particular configuration. The dungeon's random stream is access from within the selector and transform rules


.. figure:: /images/tutorial/H/query_grid_GetRandomCellOfType.png
   :align: center

   Get Random Cell Of Type


Contains Stair Between
######################

Check if there is a stair connecting the two input cells


.. figure:: /images/tutorial/H/query_grid_ContainsStairBetween.png
   :align: center

   Contains Stair Between


Contains Door Between
#####################

Check if there is a door connecting the two input cells


.. figure:: /images/tutorial/H/query_grid_ContainsDoorBetween.png
   :align: center

   Contains Door Between


Get Stair Between
#################

Get the stair information between the two input cells


.. figure:: /images/tutorial/H/query_grid_GetStairBetween.png
   :align: center

   Get Stair Between


Get Opening Point Between Adjacent Cells
########################################

When two cells are adjacent to each other, there might be a constraint on how we can traverse through them. There might be a height variation, or there might be a wall between the cells.  In that case, the only valid way to move across is through the stair or a door repectively.   This function calculates and returns the correct world position.  This position lies in the edge of the two cells.  If there is no barrier between the two cells (doors / stairs) a point in the center of the edge is returned


.. figure:: /images/tutorial/H/query_grid_GetOpeningPointBetweenAdjacentCells.png
   :align: center

   Get Opening Point Between Adjacent Cells

This function is used in the path demo to correctly place the spline through the doors and stairs


.. figure:: /images/tutorial/H/query_grid_path.jpg
   :align: center

   Query path between two cells


Get Adjacent Cells On Edge
##########################


.. figure:: /images/tutorial/H/query_grid_GetAdjacentCellsOnEdge.png
   :align: center

   Get Adjacent Cells On Edge

You can use this function in a selector logic of a marker that is on the edge (e.g. Walls / Fence).   This function returns the cells adjacent to the marker.   You can use it to decorate your walls / fence selectively. E.g. do no spawn lights on walls of an empty side, or have a different art style when a wall is shared by two rooms

Is Near Marker
##############


.. figure:: /images/tutorial/H/query_grid_IsNearMarker.png
   :align: center

   Is Near Marker

The function returns true if a marker with the specified name is found nearby.    You specify the distance to search and the marker name. 

This function is useful if you don't want to place blocking items near doors / stairs.


.. figure:: /images/tutorial/H/query_grid_near_marker_1.png
   :align: center

   Query System

.. figure:: /images/tutorial/H/query_grid_near_marker_2.png
   :align: center

   Query System



Event Listeners
---------------

Event listeners are blueprints that get notified on various dungeon events. These are great for pre / post initializations

Creation
^^^^^^^^

Create a Event listener blueprint by choosing `DungeonEventListener` as the base class

.. figure:: /images/tutorial/H/event_listener_create.png
   :align: center

   Event Listener

Override any of the function events to get notified.  This function will be called by Dungeon Architect if your blueprint is registered with the Dungeon actor

.. figure:: /images/tutorial/H/event_listener_create2.png
   :align: center

   Event Listener


Registration
^^^^^^^^^^^^

You need to register this blueprint with the dungeon actor to get its event notifications

Select the Dungeon Actor and Navigate to the `Advanced` category in the Details tab and choose your blueprint class

.. figure:: /images/tutorial/H/event_listener_create3.png
   :align: center

   Event Listener


Event Callbacks
^^^^^^^^^^^^^^^

Your blueprint can hook into various events of the dungeon build / destroy phase

On Pre Dungeon Build
####################

This is called before the dungeon is built


On Dungeon Layout Built
#######################

This is called after the dungeon layout is built in memory.  At this stage, no markers are emitted on the scene and nothing is spawned.  However, the layout is available in the dungeon model if you'd like to view or modify it


On Markers Emitted
##################

This event is called after all the markers are emitted in the scene.   This event is also called right before the Theming engine is executed.    So this event gives you an oppertunity to modify the low markers themselves

This could be useful for automatically clamping dungeon items on a landscape or to apply some filter on the markers like the one shown below (see quick start guide for an example)


.. figure:: /images/tutorial/H/event_listener_filter.jpg
   :align: center

   Event Listener


On Post Dungeon Build
#####################

This is called after the dungeon is fully built


On Pre Dungeon Destroy
######################

This is called right before the dungeon is about to be destroyed

On Dungeon Destroyed
#####################

This is called after the dungeon is fully destroyed



Landscape Transformer
---------------------

Using the Landscape Transformer, you can modify a landscape's height and weights (textures) around the dungeon's layout

The landscape transformer is implemented as a event listener, so you'll need to register it in the Dungeon actor's event listener list under the Advanced category


.. figure:: /images/tutorial/H/landscape_transformer.png
   :align: center

   Landscape Transformer

After setting the landscape transformer, expand it and set the Landscape you'd wish to modify


.. figure:: /images/tutorial/H/landscape_transformer2.png
   :align: center

   Landscape Transformer

Under the Layers array, add two entries

The first entry should be the Layer Info for filling the entire area
The second entry is for the inner path way.

You would have already created these layer info assets while creating the landscape and setting up the material

To find where you layer info is, Navigate to the Landscape tab > Paint section.  There you'd see entries for each layer that was defined in your material.   If you didn't create a layer info yet, create one or click the Find icon to find where it is.  Then assign the appropriate layer


.. figure:: /images/tutorial/H/landscape_transformer_layer.png
   :align: center

   Landscape Transformer


YOUTUBE(9MI9IzNytuY)




Navigation
----------

Unreal Engine supports runtime navigation generation.   However, a flag needs to be set in the projects setting.

Navigate to `Edit > Project Settings > Navgation Mesh > Runtime > Dynamic`


.. figure:: /images/tutorial/H/navmesh_1.png
   :align: center

   Runtime Navigation Mesh Generation


.. figure:: /images/tutorial/H/navmesh_2.png
   :align: center

   Runtime Navigation Mesh Generation

This will automatically regenerate the navigation on runtime generated dungeons.  Be sure to have a `Nav Mesh bounds Volume` large enough to wrap the whole dungeon.  There is an example in the quick start guide to automatically wrap the navigation volume around a dungeon after it has been built.

YOUTUBE(uowWAVwEiEc)



