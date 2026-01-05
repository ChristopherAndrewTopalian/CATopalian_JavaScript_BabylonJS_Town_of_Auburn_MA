// Resolution Setting for BabylonJS

In Babylon.js, you don't use `ct.scale(ratio, ratio)` because you aren't drawing individual 2D shapes manually; the 3D engine handles the "drawing" for you.

Instead, Babylon.js has a built-in way to handle high-resolution screens (Retina/4K TVs) called **Hardware Scaling**.

### The Babylon.js Solution

To get crisp edges on your big TV, you have two simple ways to implement this.

#### Method 1: The "Auto" Way (Recommended)

When you first create your Babylon Engine, you can pass an option called `adaptToDeviceRatio`. This tells Babylon to automatically check your TV's resolution and scale everything perfectly for you.

```javascript
// Add 'true' as the 4th parameter in the Engine constructor
let engine = new BABYLON.Engine(canvas, true, null, true); 

```

*The fourth parameter is `adaptToDeviceRatio`. If you set this to **true**, Babylon handles the blurry canvas issue for you automatically.*

---

#### Method 2: The Manual Way (The `ct.scale` equivalent)

If you've already initialized your engine and don't want to change the constructor, you can use the `setHardwareScalingLevel` method. This is the direct 3D equivalent of the `ct.scale` math we did earlier.

```javascript
// 1. Get the TV's pixel ratio (usually 2.0 or 3.0)
let ratio = window.devicePixelRatio || 1;

// 2. Set the scaling level. 
// Note: In Babylon, 1.0 is default. 0.5 makes it 2x sharper. 
// The formula is 1 / ratio.
engine.setHardwareScalingLevel(1.0 / ratio);

```

### Why does this fix it?

In 2D Canvas, we scaled the *drawing context*. In Babylon (which uses WebGL), we are scaling the **Render Target**.

* **Without this:** Your 300x300 canvas is rendered at low resolution and then "stretched" to fit the high-density pixels on your TV (Blurry).
* **With this:** Babylon renders the 3D scene at the *physical* resolution of the TV, so every edge of your 3D models lands perfectly on a physical pixel (Crisp).

### Professional Tip: The Resize Listener

If you are using a big TV: if you ever resize the window or move it to a different screen, the canvas might get blurry again. Always include this snippet in your `whenLoaded` function:

```javascript
window.addEventListener("resize", function () {
    engine.resize();
});

```

---

# Here is another way that we can define the engine variable

```javascript
let createDefaultEngine = function()
{
    return new BABYLON.Engine(canvas, true, 
    {
        preserveDrawingBuffer: true,
        stencil: true,
        disableWebGL2Support: false
    }, 
    true); // 'true' here for adaptToDeviceRatio
};
```

This results us very crisp looking edges and textures.

//----//

// Dedicated to God the Father  
// All Rights Reserved Christopher Andrew Topalian Copyright 2000-2026  
// https://github.com/ChristopherTopalian  
// https://github.com/ChristopherAndrewTopalian  
// https://sites.google.com/view/CollegeOfScripting

