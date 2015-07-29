# Getting started

Great! You have setup your IDE and are ready to get started creating!

## Game class

The first thing to do is to create your main game class. The game class is the main contact point between
the engine and your code. Everything should be communicating through this class!

Create a new package, for example: `io.github.yourusername` and create the java file
`MyFirstGame.java`.

### Sample code
Ready to copy and paste!

```java
package io.github.yourusername;

import org.achtern.AchternEngine.core.CoreEngine;
import org.achtern.AchternEngine.core.Game;
import org.achtern.AchternEngine.core.Transform;
import org.achtern.AchternEngine.core.math.Vector3f;
import org.achtern.AchternEngine.core.rendering.Color;
import org.achtern.AchternEngine.core.rendering.Dimension;
import org.achtern.AchternEngine.core.rendering.RenderEngine;
import org.achtern.AchternEngine.core.scenegraph.Node;
import org.achtern.AchternEngine.core.scenegraph.entity.Camera;
import org.achtern.AchternEngine.core.scenegraph.entity.controller.FlyMover;
import org.achtern.AchternEngine.core.scenegraph.entity.controller.HumanMover;
import org.achtern.AchternEngine.core.scenegraph.entity.controller.MouseLook;
import org.achtern.AchternEngine.core.scenegraph.entity.renderpasses.light.DirectionalLight;
import org.achtern.AchternEngine.core.util.FigureProvider;
import org.achtern.AchternEngine.lwjgl.bootstrap.LWJGLBindingProvider;

public class MyFirstGame extends Game {
  
  public static void main(String... args) throws Exception {
    CoreEngine engine = new CoreEngine(new MyFirstGame(), new LWJGLBindingProvider());
    engine.start(100);
    System.exit(0);
  }
  

  @Override
  public Dimension getWindowDimensions() {
    return Dimension.HD_720;
  }

  @Override
  public void init(CoreEngine engine) {
    add(new Node("Camera")
          .add(new Camera()) // the main camera
          .add(new MouseLook(1)) // allows you to look around
          .add(new HumanMover(10)) // allows you to walk
          .add(new FlyMover(10)) // allows you to fly. Awesome \o/
    );
    add(new FigureProvider("Meshes", "floor", "grid").get()); // add a basic plane mesh

    Node lights = new Node("Lights");
    lights
        .add(new DirectionalLight(Color.WHITE, 1)) // some light!
        .add(new AmbientLight(0.4f, 0.4f, 0.4f));

    add(lights);
  }

  @Override
  public void render(RenderEngine renderEngine) { }

  @Override
  public void update(float delta) { }
}

```

Do not worry we will get later into the code and discuss why we setup the class this way.

For now run this class and see what happens. You can move around by using the WASD keys and
SHIFT to fly down and SPACE to fly up. The mouse can be used to look around, after you have clicked
the game window.

You should see something like this:

![Game screen](https://i.imgur.com/6Joum8V.jpg)

If you cannot see the plane, try to fly backwards a bit. The plane is getting rendered only when
viewed from one side.

### The how and why? Learning the basics

#### Structure of an AchternEngine game

As explained above the most important class of any game that is build on top of AchternEngine is your `Game` class.

```java
public class MyFirstGame extends Game {
```

This `Game` which you extended in this example is the entry point to AchternEngine, it handles communication
between the `CoreEngine` and your code and provides the __scenegraph__ of your game.

As in most java applications you start your game with a main method

```java
public static void main(String... args) throws Exception {
  CoreEngine engine = new CoreEngine(new MyFirstGame(), new LWJGLBindingProvider());
  engine.start(100);
  System.exit(0);
}
```

Here you can see that you've created a new `CoreEngine` instance and pass in a new instance of your game.
This means also, that you games constructor cannot do anything releated to the AchternEngine, it is getting
replaced by the `#init()` method (more on that later)!

AchternEngine can be used with mulitple graphics libraries, but it is getting shipped with
[LWJGL 2](http://legacy.lwjgl.org/) bindings.

After constructing the `CoreEngine` you have to start it, by calling `CoreEngine#start()` and giving an
max frames per second. A value of 100 is in most cases sufficient.

Please make sure to call `System.exit(0);` as the last statement. Sometimes the native bindings still hang around
and won't end the process, even if the window has already vanished.

#### init() Method

__COMING SOON_
