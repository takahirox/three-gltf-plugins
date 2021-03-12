# three-gltf-extensions

[![npm version](https://badge.fury.io/js/three-gltf-extensions.svg)](https://badge.fury.io/js/three-gltf-extensions)

[Three.js](https://threejs.org) glTF [loader](https://threejs.org/docs/#examples/en/loaders/GLTFLoader) and [exporter](https://threejs.org/docs/#examples/en/exporters/GLTFExporter) have plugin system to provide extensibility mechanism to users. glTF extensions can be handled with the plugin system.

Some plugins for major and stable extensions are built-in in the loader and exporter. But other extensions are not supported as built-in by them (yet) because for example the specification is not great fit to Three.js API or structure, or the specification is not finalized.

If you want to use such extensions you need to write plugins by yourself but it requires the knowledge of glTF specification, extensions specification, Three.js core API, or Three.js glTF loader/exporter API. It can be difficult for some users.

This project provides you Three.js glTF loader/extension plugins even for such extensions. You no longer need to write the plugin on your own.

## Goals

* Provide reusablity and easiness to use even for the the extensions the spec of which isn't great fit to Three.js API or structure
* Allow early trial of glTF extensions the spec of which is not finalized yet
* Send feedback to Three.js glTF loader/exporter plugin system APIs

## Online demo

* [Online demo](https://rawcdn.githack.com/takahirox/three-gltf-extensions/cf44f0e1d0b3a4e9d6716a9ae769a1bd06a00592/examples/index.html)

## Supported glTF extensions

* [KHR_materials_variants](https://github.com/KhronosGroup/glTF/tree/master/extensions/2.0/Khronos/KHR_materials_variants)
* [EXT_text](https://github.com/takahirox/EXT_text) (Loader only)
* [MSFT_lod](https://github.com/KhronosGroup/glTF/tree/master/extensions/2.0/Vendor/MSFT_lod) (Loader only, in progress)
* [MSFT_texture_dds](https://github.com/KhronosGroup/glTF/tree/master/extensions/2.0/Vendor/MSFT_texture_dds) (Loader only)

## Compatible Three.js revision

&gt;= r126

## How to use

**GLTFLoader plugins**

```javascript
// Import Three.js
import * as THREE from 'path_to_three.module.js';
import {GLTFLoader} from 'path_to_GLTFLoader.js';

// Import three-gltf-extensions loader plugins
import GLTFFooExtension from 'path_to_three-gltf-extensions/loaders/Foo_extension/Foo_extension.js';

// Register the plugin to the loader and then load glTF
const loader = new GLTFLoader();
loader.register(parser => new GLTFFooExtension(parser));
loader.load(path_to_gltf_asset, gltf => {
  ...
});
```


**GLTFExporter plugins**

```javascript
// Import Three.js
import * as THREE from 'path_to_three.module.js';
import {GLTFExporter} from 'path_to_GLTFExporter.js';

// Import three-gltf-extensions exporter plugins
import GLTFExporterFooExtension from 'path_to_three-gltf-extensions/exporters/Foo_extension/Foo_extension_exporter.js';

// Register the plugin to the exporter and then export Three.js objects
const exporter = new GLTFExporter();
exporter.register(writer => new GLTFExporterFooExtension(writer));
exporter.parse(scene, result => {
  ...
});
```

Refer to each plugin's README for more detail.


## Locally run examples

```sh
$ npm install
$ npm start
# Access http://localhost:8080/examples/index.html
```

## Unit Test

### Unit Test on Web browser

```sh
$ npm install
$ npm run test-install
$ npm run test-build
$ npm start
# Access http://localhost:8080/test/index.html
```

### Unit Test on Node.js


```sh
$ npm run test-install
$ npm run test
```

Note that the unit tests which rely on Web don't run. I recommend to run the unit tests on Web browser.

## Customize the plugins in your side

As written above, some extensions are not great fit to Three.js API or structure. So the plugins for them may have some limitations. If they don't cover your use case, please fork the repository and customize in your side.
