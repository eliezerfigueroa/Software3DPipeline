# Rudimentary 3D Software Rendering Pipeline

This project is a simple, from-scratch implementation of a 3D software rendering pipeline in vanilla JavaScript. It renders a rotating 3D cube on an HTML5 canvas without using WebGL or any other graphics libraries. The primary goal is to demonstrate the fundamental mathematical concepts behind 3D graphics in a clear and modular way.

## File Structure

*   `index.html`: The main HTML file containing the `<canvas>` element where the 3D scene is rendered.
*   `main.js`: Contains all the JavaScript code for the rendering pipeline, including data structures, scene setup, pipeline transformations, and the main render loop.
*   `README.md`: This file.

## General Architecture

The rendering process is broken down into a "pipeline" of distinct stages. A 3D model (a "mesh") starts as a set of vertices in its own coordinate system (local space). These vertices are processed through the pipeline stages until they are finally drawn as 2D shapes on the screen.

The pipeline is implemented in `main.js` and consists of the following key components:

### Data Structures
*   `Vector3`: A class representing a point or vector in 3D space (x, y, z).
*   `Mesh`: A class that holds the geometry of an object, defined by an array of `vertices` and an array of `faces`.

### Pipeline Stages
1.  **Model Transformation (`modelTransform`)**: The cube's vertices are rotated in 3D space. This transforms the object from its local space (centered at the origin) into the "world space".
2.  **View Transformation (`viewTransform`)**: The entire world is positioned relative to a camera. In this simple implementation, this is achieved by just moving the cube away from the camera's position along the Z-axis so it is visible.
3.  **Projection Transformation (`projectionTransform`)**: The 3D coordinates from the view space are projected onto a 2D plane. This project uses perspective projection (`x' = x/z`, `y' = y/z`), which makes objects that are farther away appear smaller.
4.  **Rasterization (`rasterize`)**: The final 2D points are used to draw lines on the canvas. This stage iterates through the cube's faces, connects the projected vertices with lines, and "draws" the final wireframe image.

### The Render Loop
An animation loop, driven by `requestAnimationFrame`, continuously performs these steps:
1.  Clears the canvas.
2.  Updates the cube's rotation angle.
3.  Passes all of the cube's vertices through the pipeline (Model -> View -> Projection).
4.  Calls the rasterizer to draw the final result.

## Limitations

This project is for educational purposes and is intentionally minimalistic. It lacks many features of a full rendering engine, such as:

*   **Lighting and Shading**: All lines are drawn with a single color. There is no concept of light sources or how they affect the color of the cube's faces.
*   **Texturing**: The faces are not filled, and no images (textures) are mapped onto them.
*   **Hidden Surface Removal**: The cube is drawn as a wireframe. In a solid object, you would not be able to see the back faces. This pipeline does not perform culling or use a z-buffer to determine which faces are in front of others.
*   **Clipping**: Vertices or faces that go behind the camera's near plane are not correctly handled, which can cause visual artifacts (like the object inverting) if it gets too close to the camera origin.
