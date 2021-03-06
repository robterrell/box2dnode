# box2dnode

@author Josh Adell <josh.adell@gmail.com>

A port of the box2djs library into a node module.

## Install

Two options here:

1) Grab the code from its <http://github.com/jadell/box2dnode>

2) Use npm: `npm install box2d`

Option 2 is the recommended way.

## Code example

Here is the box2d "Hello World" program from http://www.box2d.org/ written for node:

    var sys = require("sys"),
        b2d = require("./box2dnode");
    
    // Define world
    var worldAABB = new b2d.b2AABB();
    worldAABB.lowerBound.Set(-100.0, -100.0);
    worldAABB.upperBound.Set(100.0, 100.0);
    
    var gravity = new b2d.b2Vec2(0.0, -10.0);
    var doSleep = true;
    
    var world = new b2d.b2World(worldAABB, gravity, doSleep);
    
    // Ground Box
    var groundBodyDef = new b2d.b2BodyDef();
    groundBodyDef.position.Set(0.0, -10.0);
    
    var groundBody = world.CreateBody(groundBodyDef);
    
    var groundShapeDef = new b2d.b2PolygonDef();
    groundShapeDef.SetAsBox(50.0, 10.0);
    
    groundBody.CreateShape(groundShapeDef);
    
    // Dynamic Body
    var bodyDef = new b2d.b2BodyDef();
    bodyDef.position.Set(0.0, 4.0);
    
    var body = world.CreateBody(bodyDef);
    
    var shapeDef = new b2d.b2PolygonDef();
    shapeDef.SetAsBox(1.0, 1.0);
    shapeDef.density = 1.0;
    shapeDef.friction = 0.3;
    body.CreateShape(shapeDef);
    body.SetMassFromShapes();
    
    // Run Simulation!
    var timeStep = 1.0 / 60.0;
    
    var iterations = 10;
    
    for (var i=0; i < 60; i++) {
        world.Step(timeStep, iterations);
        var position = body.GetPosition();
        var angle = body.GetAngle();
        sys.puts(i+": <"+position.x+", "+position.y+"> @"+angle);
    }

