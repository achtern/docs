# Scenegraph

The scenegraph houses every component you might have in your game, from 3d models over lights to sounds
and cameras. A scenegraph consists of a `Node` objects and these nodes hold `Entity` objects.

The scenegraph is just a graph of these nodes. The `Game` class is handling the root node for you,
you cannot access this root node directly.

In order to add your components to the scenegraph the `Game` class provides the `add()` method or to get
components from the scenegraph a `get()` method. The game just forwards calls to these methods to the root
node.

## Nodes and Entities

Nodes, often called components, are the building blocks of the scenegraph, they are doing
the heavy lifting of managing change, storing references to different AchternEngine parts, etc.

Entities on the other hand are things that the user sees, interacts, heres or influences any of the
previous. Entities are any 3D geometry, light, sound source/emitter, fog and even input handlers.

Entities are not part of the scenegraph directly! An entity is added to Node before hand; entities cannot
have any children, only the __parent node__.

In your `MyFirstGame` class we start of by __adding__ a `Node` which will hold the `Camera` `Entity`
and some more stuff.

Every Node has a name associated with it, even if you do not name a node it will get a generic name,
e.g. _Untitled Node 1_.

## Transform

It would be pretty boring if every object in your scene would have the same position, this is why
every __node__ has its own `Transform` associated with it, all entities inherit this transform.
This transform data is __relative__ to the transform of the parent node in the graph,
this _"relativity"_ propagates all the way up to the root node which has the
absolute coordinates of `(0/0/0)`, being the center of the 3D world.

__All entites in a node share the same transform!__

Keep this mind! If you want to have for example two 3D models on top of each other, each will need it's own node.
You can then add these two nodes to another parent node, in order to move them both at the same time.

A Transform consists of a _position_, _rotation_ and _scale_.
