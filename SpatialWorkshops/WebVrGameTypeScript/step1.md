# Introducing BabylonJS with TypeScript

In this workshop you will learn how to build a Web VR game with BabylonJS and [TypeScript](https://typescriptlang.org).

![game img](https://imgur.com/bvJslJf.jpg)

## Prerequisites

- [Node.js](https://nodejs.org/en/download/)
- [Visual Studio Code](https://code.visualstudio.com/download?WT.mc_id=devto-blog-casiljan)

### What is BabylonJS and CannonJS?

[BabylonJS](https://www.babylonjs.com/) is a complete JavaScript framework for building 3D games and experiences with HTML5, [WebGL](https://en.wikipedia.org/wiki/WebGL), WebVR and Web Audio.

[CannonJS](http://www.cannonjs.org/) is a physics engine, written in JavaScript. And what is a physics engine you might ask? Well its "software that provides an approximate simulation of certain physical systems, such as rigid body dynamics (including collision detection), soft body dynamics, and fluid dynamics, of use in the domains of computer graphics, video games and film."

### What is TypeScript?

[TypeScript](https://www.typescriptlang.org/) is a typed superset of JavaScript the compiles to plain JavaScript. TypeScript starts from the same syntax and semantics that millions of JavaScript developers know today. Use existing JavaScript code, incorporate popular JavaScript libraries, and call TypeScript code from JavaScript.

TypeScript compiles to clean, simple JavaScript code which runs on any browser, in Node.js, or in any JavaScript engine that supports [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) 3 (or newer).

## Getting started

First we need to get the base starter project using BabylonJS, [Webpack](https://webpack.js.org/concepts/), and TypeScript

Steps to Run Starter Project and [Git Repo Link](https://github.com/cassieview/babylonjs-webpack-typescript-starter-project)

1. Clone the repo and change directories  
   `git clone https://github.com/cassieview/babylonjs-webpack-typescript-starter-project.git`  
   `cd babylonjs-webpack-typescript-starter-project`
2. Install packages  
   `npm install`
3. Build Project  
   `npm run build`
4. Run the script to test the project  
   `npm start`
5. Open in VS Code  
   `code .`

## Starter project

Let's talk about the starter project

### Simple index.html template

The template includes a canvas which will act as the container for our application.

``` html
<!DOCTYPE html>
<html>

    <head>
        <style>
            html,
            body {
                overflow: hidden;
                width: 100%;
                height: 100%;
                margin: 0;
                padding: 0;
                text-align: center;
            }

            #renderCanvas {
                width: 100%;
                height: 100%;
                touch-action: none;
            }
        </style>
    </head>

    <body>
        <canvas id="renderCanvas"></canvas>
        <script src="dist/index.js"></script>
    </body>

</html>
```

### The index.ts TypeScript file

The `index.ts` file is the TypeScript file that creates the main scene. When you run `npm run build` it is to compiled to vanilla JavaScript in the dist folder. This is then called with the `script` tag in the `index.html`.

The script source for the game is found in the dist folder. Webpack is an open-source JavaScript module bundler it generates static assets representing those modules. This is what is loaded from the dist folder. WebPack compiles the script down to one source and that is used to serve the game script.

The below script shows how we import the packages needed from BabylonJS to create our game scene. Create the canvas variable and use vanilla JavaScript to grab the renderCanvas canvas tag from the html body section. Then we create the engine variable and pass in the new BabylonJS Engine.

``` javascript
import { Engine, Scene, HemisphericLight, Vector3, MeshBuilder, Mesh } from "babylonjs";
var canvas: any = document.getElementById("renderCanvas");
var engine: Engine = new Engine(canvas, true);
```

Below we have the create scene function. Here we define the `scene`, pass in the `engine`. Then we create a camera. The camera is the point of view of the game player. We are using the [free camera]("https://doc.babylonjs.com/babylon101/cameras#free-camera").

Next we add a simple sphere `mesh` to our scene and set the basic properties such as size, name and the scene we created.

The VR helper adds the VR button to the bottom right of the screen so that a user can enter the game in vr for a web browser.

TIP: You can easily test changes as you make them by running `npm run build` then open the path to the `index.html` file in the browser `../babylonjs-webpack-typescript-starter-project/index.html`. This is a static site so you don't actually have to run it with `npm start`. Simply run the build and refresh the browser path to the `index.html`.

```javascript
function createScene(): Scene {
    // Create scene
    var scene: Scene = new Scene(engine);

    // Create camera
     var camera = new BABYLON.FreeCamera("Camera", new BABYLON.Vector3(0, 0, -10), scene);

    // Create sphere
    var sphere1: Mesh = MeshBuilder.CreateSphere("sphere", { diameter: 1 }, scene);
    sphere1.position.y = 5;
    sphere1.material = new BABYLON.StandardMaterial("sphere material", scene)

    // Enable VR
    var helper = scene.createDefaultVRExperience({createDeviceOrientationCamera: false});
    helper.enableInteractions();

    return scene;
}

var scene: Scene = createScene();

engine.runRenderLoop(() => {
    scene.render();
});
```

<button name="button" onclick=".\step2.md">Next Step</button>
