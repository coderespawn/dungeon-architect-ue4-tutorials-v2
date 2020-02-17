Create your first Dungeon
=========================

Install Dungeon Architect
-------------------------

Install `Dungeon Architect <https://www.unrealengine.com/marketplace/en-US/product/dungeon-architect>`_ from the UE4 Marketplace

.. image:: /images/tutorial/A/01.jpg
   :align: center

Setup Dungeon Actor
-------------------

Create a new Level and drop in a Dungeon actor

.. image:: /images/tutorial/A/02.jpg
   :align: center


Assign Theme
------------

A theme file defines the assets to use to build the dungeon.  Assign an existing theme to the dungeon actor

Select the dungeon actor and inspect the Details panel

Add a new Theme entry by clicking the plus icon.
 
.. image:: /images/tutorial/A/03.png
   :align: center
   

Enable ``Show Plugin Content`` from the **View Options** so we can see our sample theme

.. image:: /images/tutorial/A/04A1.png
   :align: center
   
.. image:: /images/tutorial/A/04A2.png
   :align: center
   
.. image:: /images/tutorial/A/04A3.png
   :align: center

Search for ``candy`` and select the candy theme

.. image:: /images/tutorial/A/04.png
   :align: center

.. image:: /images/tutorial/A/04A4.png
   :align: center


Build Dungeon
-------------

* Select the Dungeon actor and inspect the Details Panel
* Click ``Build Dungeon`` button to generate the dungeon

.. image:: /images/tutorial/A/05.png
   :align: center

.. image:: /images/tutorial/A/06.jpg
   :align: center

Randomize Dungeon
-----------------

 * Select the Dungeon actor and inspect the Details Panel
 * Click ``Randomize Seed``
 * Click ``Build Dungeon`` to generate a new dungeon with a different layout
 


.. image:: /images/tutorial/A/07.png
   :align: center

.. image:: /images/tutorial/A/08.jpg
   :align: center

The ``Randomize Seed`` button is a helper function which simply changes the ``Seed`` value in the dungeon configuration.  Changing the ``Seed`` value changes the layout of the dungeon.    If you assign a random value to a seed and build, you'll get a new dungeon layout

.. image:: /images/tutorial/A/09.png
   :align: center
   
Organization
------------

When you build a dungeon, all the spawned dungeon actors are placed under a folder named after the dungeon actor's label

.. image:: /images/tutorial/A/10.png
   :align: center


 


