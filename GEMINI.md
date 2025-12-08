# Project Context: Rudimentary 3D Rendering Pipeline

## 1. Objective

This project implements a basic 3D rendering pipeline from scratch using pure JavaScript and the HTML5 Canvas API. The goal is to render a rotating 3D cube without relying on WebGL or any external graphics libraries like Three.js. This approach is intended for educational purposes, to demonstrate the fundamental mathematical principles behind 3D graphics.

## 2. Core Concepts: The Rendering Pipeline

The rendering process is broken down into several distinct stages, each handled by a specific function to ensure clarity and modularity.

### Data Structures
*   **`Vector3`**: Represents a point in 3D space (x, y, z).
*   **`Mesh`**: Represents a 3D object, containing a list of vertices (the points) and faces (the connections between vertices).

### Pipeline Stages
1.  **Model Transformation**: The `Mesh`'s vertices are first transformed from their local (or model) space into world space. In this project, this involves applying a rotation matrix to each vertex to make the cube spin.
2.  **Camera/View Transformation**: The world-space coordinates are then transformed into camera (or view) space. This stage positions the world relative to the camera. For simplicity, this project achieves this by offsetting the object along the Z-axis to place it in front of the camera.
3.  **Projection Transformation**: The 3D coordinates from the camera view are projected onto a 2D plane. This project uses perspective projection, where an object's apparent size is inversely proportional to its distance from the camera. The core mathematical operation is dividing the X and Y coordinates by the Z coordinate ($x' = x/z$, $y' = y/z$).
4.  **Rasterization**: The final 2D points are drawn onto the canvas. This stage involves connecting the projected vertices with lines (`ctx.lineTo`) to form the edges of the cube.

## 3. Implementation Details

*   **Animation Loop**: A `requestAnimationFrame` loop is used to continuously update the scene. In each frame, the canvas is cleared, the cube's rotation angle is updated, all vertices are processed through the pipeline, and the resulting 2D shape is drawn.
*   **Scene**: The scene consists of a single `Mesh`: a cube centered at the origin (0,0,0) with defined vertices and faces.
*   **Rendering**: The output is a wireframe rendering of the cube, drawn with black lines on a white background for clarity.

## 4. Project Structure

The project is organized into separate HTML and JavaScript files to distinguish presentation from logic.

*   **`index.html`**: The main entry point of the application. It contains the HTML boilerplate and a `<canvas>` element where the 3D scene is rendered. It includes the `main.js` script.
*   **`main.js`**: Contains the entire JavaScript logic for the 3D pipeline, including the data structures (`Vector3`, `Mesh`), pipeline functions (transformations, projection), scene definition, and the main animation loop.
*   **`README.md`**: Provides an overview of the project, setup instructions, and a description of the files.
