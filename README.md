# Magic Leap Floor Detection ![stability-wip](https://img.shields.io/badge/stability-work_in_progress-lightgrey.svg)

Detect and display the floor in Magic Leap Unity projects with this expansion to the ML SDK Meshing example scene.

## Dependencies

* Lumin SDK v0.20.0.
* Magic Leap Unity® Package v0.20.0.
* Unity 2019.1.5f1 with Lumin OS (Magic Leap) Build Support.

It will likely work in other versions of Unity 2019, but I make no guarantees. 😎

## How to Use

All Magic Leap code and content is .gitignored so as to abide by the terms of the Independent Creator Program.

To use this example, either (in order of simplicity):

1. Import [MagicLeapFloorDetection.unitypackage](https://github.com/davidfoster/magic-leap-floor-detection/blob/develop/Packages/MagicLeapFloorDetection.unitypackage) into an existing ML Unity project.
2. Import the ML Unity package included with the SDK into the project under [_Projects/MagicLeapFloorDetection_](https://github.com/davidfoster/magic-leap-floor-detection/blob/develop/Projects/MagicLeapFloorDetection), then import ML Remote support libraries ("_Magic Leap > ML Remote > Import Support Libraries_" menu item inside of Unity).
   * Make sure the Lumin platform is active in Build Settings or you will receive a "No ML VRDevice loaded" error.

## Examples

In these examples, vertices are rendered in yellow whose normals fall within a specified degree delta of the floor normal. Of those vertices, those who fall below the detected floor y are considered to be a part of the floor, and are rendered in green.

By default, the degree delta is `20`° and the floor normal is world `Vector3.up`. The rendered detected floor y also includes an error margin (default: `0.05`) to envelop noise in the spatial map which falls just above the de facto detected floor y but should still be considered a part of the floor.

### Simple Floor Visualizer

<img src="https://github.com/davidfoster/magic-leap-floor-detection/blob/develop/Examples/simple-floor-visualizer-example.png" alt="Simple Floor Visualizer." width="392" height="294" />

### Spatial Mapper Meshing Wireframe

<img src="https://github.com/davidfoster/magic-leap-floor-detection/blob/develop/Examples/spatial-mapper-meshing-wireframe-example.png" alt="Spatial Mapper Wireframe Occlusion." width="392" height="294" />

### Spatial Mapper Meshing Occlusion

In this example, the spatial mapper meshing visualizer is not actually rendering the green. The green is coming from a separate quad located under the world. Because the meshing visualizer in occlusion mode renders pixels to the depth buffer (`ZWrite On`), we actually want to discard vertices considered to belong to the floor so they do not occlude objects under the floor.

Vertex 'discarding' is done in the vertex program by performing an invalid operation on the vertex position (division by zero). This behaviour is undefined but works in OpenGL ES and OpenGL Core and is much more performant than a true `discard` in the fragment program because it avoids a branching operation.

<img src="https://github.com/davidfoster/magic-leap-floor-detection/blob/develop/Examples/spatial-mapper-meshing-occlusion-example.png" alt="Spatial Mapper Meshing Occlusion." width="392" height="294" />

## License

This project is licensed under the [MIT license](https://github.com/davidfoster/magic-leap-floor-detection/blob/develop/LICENSE).