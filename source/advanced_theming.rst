Advanced Theming
================

Theming Rules
-------------

You can attach Blueprint (or C++) based logic on the theme nodes for more control. There are two types of rules you can attach to Visual nodes


.. figure:: /images/tutorial/G/rules_01.png
   :align: center

   Visual Node Rules

Selection Rule
--------------
A selection rule is a blueprint class (or C++ class) that is used to decide if the current node is to be attached to the scene.  This rule replaces the default **Probability** property that is used for randomly deciding if visual node needs spawning based on a probability.

Selection rules gives you more power, when you need it.   In the rule's blueprint logic, you can query the dungeon model and determin if this node should be inserted into the scene

Using Selection Rules
^^^^^^^^^^^^^^^^^^^^^
To assing an existing rule into the node, Check the **Use Selection Logic** property and select the rule you would like to attach to the node from the dropdown list


.. figure:: /images/tutorial/G/selection_rule_01a.png
   :align: center

   Assign an existing Selection Rule

Create a new selection rule by creating a new blueprint class derived from the appropriate DungeonSelectorLogic.  It should match the builder you are targeting


.. figure:: /images/tutorial/G/create_rule_transform1.png
   :align: center

   Create a new Selection Rule

Open up the blueprint and override the **Select Node** function. This function will be called by the engine and the logic you put here will let you decide if the node should to be selected


.. figure:: /images/tutorial/G/selection_rule_04.png
   :align: center

   Override function to define logic

The selection can be combined with the Probability varaible by unchecking **Logic Overrides Probability**


.. figure:: /images/tutorial/G/selection_rule_02b.png
   :align: center

   Combine selection logic with Probability variable

Example #1
^^^^^^^^^^

Here is an example of a selection logic that selects a node only if the sum of their X and Y positions are even numbers (logic for a checkerboard pattern)


.. figure:: /images/tutorial/G/selection_rule_05.png
   :align: center

   Override function to define logic

And the result after applying this rule to the ground node:


.. figure:: /images/tutorial/G/selection_rule_06.jpg
   :align: center

   Custom selection rule attached to a mesh node

You can add more visual nodes and experiment with the **Consume on Attach** parameter to get interesting results


.. figure:: /images/tutorial/G/selection_rule_07.jpg
   :align: center

   Multiple visual nodes working together

In the above example, the first node has **Consume on Attach** checked.  So if your blueprint logic selects the node, the sandstone mesh will be inserted and the execution stops.   However if the selection node doesn't select the node, the execution will always proceed to the next node and execute the mesh which inserts a clay brick mesh


.. figure:: /images/tutorial/G/selection_rule_eg1_1.jpg
   :align: center

   
In the above example, the selection rule is applied to the golden pillar.  But whenever it is selected, it stops execution because the **Consume on Attach** variable is set and doesn't build a ground mesh there.    Unchecking **Consume on Attach** on the first node lets the execution proceed even if it is inserted into the scene

.. figure:: /images/tutorial/G/selection_rule_eg1_2.jpg
   :align: center

   



Example #2
^^^^^^^^^^
This example places a stone mesh on the ground, but only if the cell is inside a room (and not a corridor)


.. figure:: /images/tutorial/G/selection_rule_eg2_1.jpg
   :align: center

   Stone ground mesh selection only when inside rooms


.. figure:: /images/tutorial/G/selection_rule_eg2_2.jpg
   :align: center

   Room selector logic

The above Selection logic was attached to the stone mesh ground node so it gets selected only when the ground marker is inside a room

Example #3
^^^^^^^^^^
Ignore nodes that are near other markers.  This is very useful if you don't want to place blocking items near stairs, doors etc


.. figure:: /images/tutorial/G/query_grid_near_marker_1.png
   :align: center

   Query System

.. figure:: /images/tutorial/G/query_grid_near_marker_2.jpg
   :align: center

   Query System


Transform Rule
--------------

Dungeon Architect lets you specify offsets to your visual nodes to move/scale/rotate them from their relative marker locations.


.. figure:: /images/tutorial/G/offset.png
   :align: center

   Static node Offset


However, if you want a more dynamic way of applying offsets (based on blueprint or C++ logic), you can do so with a *Transform Rule*.  This can be very useful to add variations to your levels for certain props


Using Transform Rules
^^^^^^^^^^^^^^^^^^^^^
To assing an existing rule into the node, Check the **Use Transform Logic** property and select the rule you would like to attach to the node from the dropdown list


.. figure:: /images/tutorial/G/transform_rule_01b.png
   :align: center

   Assign an existing Transform Rule

Create a new Transform rule by creating a new blueprint class derived from the appropriate DungeonTransformLogic.  It should match the builder you are targeting


.. figure:: /images/tutorial/G/transform_rule_01a.png
   :align: center

   Create a new Selection Rule

Open up the blueprint and override the **Get Node Offset** function. This function will be called by the engine and the logic you put here will let you decide on the offset that needs to be applied on this node


.. figure:: /images/tutorial/G/transform_rule_04.png
   :align: center

   Override function to define logic


Example #1
^^^^^^^^^^

In this example, a single rock mesh is randomly rotated, and slightly scaled and translated to give a nice cave like look


.. figure:: /images/tutorial/G/transform_rule_eg1_1.jpg
   :align: center

   Rocks randomly rotated, translated and scaled

A different transformation rule is applied to ceiling stone meshes for more variations


.. figure:: /images/tutorial/G/transform_rule_eg1_2.jpg
   :align: center

   Transform rule applied to rock nodes


.. figure:: /images/tutorial/G/transform_rule_eg1_3.png
   :align: center

   Cliff Random rotation rule

Example #2
^^^^^^^^^^

Here is an example where alternate pipes are rotated by 180 degrees to give a visually appealing look


.. figure:: /images/tutorial/G/transform_rule_eg2_1.jpg
   :align: center

   Alternate meshes are rotated by 180 degrees

This was done by rotating the mesh node by 180 degrees for every alternate cell (similar to the checker rule logic seen previously)


.. figure:: /images/tutorial/G/transform_rule_eg2_2.jpg
   :align: center

   Rule assignment


Example #3
^^^^^^^^^^

In this example a small random rotation is applied to orange ground tiles.  Useful while creating ruins when laying down broken tile meshes


.. figure:: /images/tutorial/G/vol_platform_04c.jpg
   :align: center

   Transform rule applied to orange ground meshes


.. figure:: /images/tutorial/G/transform_rule_eg3_1.png
   :align: center

   Transformation Rule Blueprint


Spawn Logic
-----------

Spawn Logics are blueprints that are attached to visual nodes and are executed whenever that visual item (mesh, actor, particle system, light etc) is spawned into the scene

These are great for initializing blueprints (or randomizing them). Some use cases include randomizing the colors of the lights that spawn from a light node, or you can use it to initialize your blueprints spawned from the actor nodes


You can attach a spawn logic to any visual node (e.g. mesh node, light node, particle system node, actor node etc)

Set the *Use Spawn Logic* flag and choose your spawn logic blueprint


.. figure:: /images/tutorial/G/spawn_logic_detail.png
   :align: center

   Spawn Logic


Create Spawn Logic
^^^^^^^^^^^^^^^^^^


.. figure:: /images/tutorial/G/spawn_logic_create.png
   :align: center

   Spawn Logic

Create a new blueprint class and pick DungeonSpawnLogic class as the parent

Define Spawn Logic
^^^^^^^^^^^^^^^^^^

Open your blueprint and override the *OnItemSpawn* function.   


.. figure:: /images/tutorial/G/spawn_logic_override.png
   :align: center

   Spawn Logic

Get the reference of the spawn actor and cast it to the type you are expecting.  Since this logic was attached to a mesh node,  it is cast to a static mesh and customizations can be applied to it 

.. figure:: /images/tutorial/G/spawn_logic_override2.png
   :align: center

   Spawn Logic


Another blueprint that was attached to a point light.  Since we expect a point light, we cast to the correct type and change the color

.. figure:: /images/tutorial/G/spawn_logic_override3.png
   :align: center

   Spawn Logic


Clustered Theming
-----------------

Clustered theming allows you to automatically apply different themes to various parts (clusters) of your dungeons. This helps in adding variation to your levels and break monotony

A continous section of corridor cells or rooms are assigned to a clusters to have a proper theme transtions 


.. figure:: /images/tutorial/G/cluster_theme.jpg
   :align: center

   Cluster Theming

Using Clustered Theming
^^^^^^^^^^^^^^^^^^^^^^^

To use clustered theming, enable it from the dungeon's detail panel


.. figure:: /images/tutorial/G/cluster_theme_enable.png
   :align: center

   Enable Cluster Theming

Once enabled, you need to define a list of theme sets you'd like to apply on the clusters from the Advanced category of the dungeon's detail panel


.. figure:: /images/tutorial/G/cluster_theme_advanced_details.png
   :align: center

   Assign Cluster Themes

.. important::
   When you use clustered themes, the **dungeon's default theme array list will be ignored** and the theme list defined in the cluster themes mapping would be used instead

Currently, only the grid builder supports clustered theming


Height Variations
^^^^^^^^^^^^^^^^^

Corridor cells connected together are grouped into a cluster.   You can customize if connected nearby corridor cells on different height (connected through stairs) should be grouped into the same cluster


.. figure:: /images/tutorial/G/cluster_theme_advanced_details.png
   :align: center

   Cluster Height Variation



.. figure:: /images/tutorial/G/cluster_theme_height1.jpg
   :align: center

   Cluster Height Variation 

.. figure:: /images/tutorial/G/cluster_theme_height2.jpg
   :align: center

   Cluster Height Variation

Notice the corridor on the bottom right.  It was split into two themes because of the height variation

Spatial Constraints
-------------------

Spatial constraints are great of checking the state of nearby tiles and using it as a condition to place items on the scene

Spatial constraints are set in the theme graph's node.   


.. figure:: /images/tutorial/G/spatial_constraint_a.jpg
   :align: center

   Spatial Constraints 

In the above example, a statue mesh is added to the ground marker.    We want this to appear only on the corners and not on each tile

Select a mesh node and in the details panel, enable *Use Spatial Constraint*

Then select the spatial constraint type.  Since this is a ground mesh, it is surrounded by 3x3 tiles


.. figure:: /images/tutorial/G/spatial_constraint2.png
   :align: center

   Spatial Constraints

Expand the spatial setup. Here you specify the rules of the adjacent tiles, whether it should be empty, occupied or should be ignored.   The rules will try to rotate to best fit the layout


.. figure:: /images/tutorial/G/spatial_constraint3.jpg
   :align: center

   Spatial Constraints

With this setup, the statues spawn only at the corners
