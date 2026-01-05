# Resolution Setting

## The Wrong Way:
```javascript
let createDefaultEngine = function()
{
    return new BABYLON.Engine(canvas, true,
    {
        preserveDrawingBuffer: true,
        stencil: true,
        disableWebGL2Support: false
    });
};
```

----

## The Right Way
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

//----//

// Dedicated to God the Father  
// All Rights Reserved Christopher Andrew Topalian Copyright 2000-2026  
// https://github.com/ChristopherTopalian  
// https://github.com/ChristopherAndrewTopalian  
// https://sites.google.com/view/CollegeOfScripting

