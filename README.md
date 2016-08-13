# THREE.CubemapToEquirectangular

Helper to extract an equirectangular panorama PNG from any three.js scene.

#### How to use ####
Include script after THREE is included
```
<script src="CubemapToEquirectangular.js"></script>
```
Define a new instance of THREE.CubemapToEquirectangular.
```
// create renderer, scene, camera, etc.
var renderer = new THREE.WebGLRenderer();
var scene = new THREE.Scene();
var camera = new THREE.Camera( /* ... */ );

// Create a managed CubemapToEquirectangular
var equiManaged = new THREE.CubemapToEquirectangular( renderer, true );

// or create an unmanaged CubemapToEquirectangular
var equiUnmanaged = new THREE.CubemapToEquirectangular( renderer, false );
```

#### Managed CubemapToEquirectangular ####
With Managed mode, the THREE.CubeCamera creation, update, render, etc. is all taken care of. You only have to call:
```
equiManaged.update( camera, scene );
```
at any point in your code that you want to extract a panorama.
The cube map created will be 4096x4096 and the exported panorama will be 4096x2048.

#### Unmanaged CubemapToEquirectangular ####
If you want to use a different CubeMap camera, or do something custom with the render, you will have to set the Unmanaged mode.

You will have to create and manage your THREE.CubeCamera:
```
var cubeCamera = new THREE.CubeCamera( .1, 1000, 4096 );
```
and manage all your scene update and rendering. When you want to export a panorama, call:
```
// this is where the developer updates the scene and creates a cubemap of the scene
cubeCamera.position.copy( camera.position );
cubeCamera.updateCubeMap( renderer, scene );

// call this to convert the cubemap rendertarget to a panorama
equiUnmanaged.convert( cubeCamera );
```

#### Changing output size ####
To export a different size, call ```setSize( width, height )```:
```
equi.setSize( 2048, 1024 );
```

#### License ####

MIT licensed

Copyright (C) 2016 Jaume Sanchez Elias, http://www.clicktorelease.com