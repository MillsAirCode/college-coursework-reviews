# CS330-ComputerGraphics-Project

https://github.com/MillsAirCode/CS330-ComputerGraphics-Project

## what it was

I built this for SNHU CS-330 (Computer Graphics). A 3D scene renderer in C++ with OpenGL 4.4 using GLFW, GLEW, GLM, and stb_image. The scene has a table top with marble texture, a book, a soap bar, a cologne bottle with cap, and two cylinders. Phong lighting with two point lights and distance attenuation. Camera moves with WASD, mouse for look, scroll wheel for speed, and P to toggle between perspective and orthographic projection. Everything lives in one Application.cpp file at around 1100 lines.

## what holds up

The shader code is clean. Vertex shader does proper MVP transforms, passes fragment position and normals to the fragment shader with the inverse-transpose normal matrix. Fragment shader has a Light struct with ambient, diffuse, specular, and attenuation parameters, loops over two point lights, and applies the Phong model with specular highlights. That's exactly how you teach OpenGL lighting.

The GLSL macro for embedding shader source as string literals is a nice pattern -- `#define GLSL(Version, Source) "#version " #Version " core \n" #Source`. Keeps shaders in the same file as the code that uses them. Works fine for a single-file project.

The cylinder helper class from Song Ho Ahn is a solid choice. Interleaved V/N/T vertex data, proper normals, separate draw methods for base/top/side. Saved me from writing cylinder geometry by hand.

## what I'd refactor

One file for everything. Application.cpp has init, input, rendering, mesh creation, shader compilation, texture loading, and cleanup all in one file. The vertex data for six objects is just a giant array literal in UCreateMesh() -- 200 lines of hardcoded floats. No scene graph, no object abstraction, no way to add a new object without appending to the array and calculating offsets by hand.

glGetUniformLocation called every frame in URender(). Those locations don't change after link time. Cache them once in init or store them in a struct. Same goes for rebuilding the projection matrix every frame -- it only changes when you press P.

Mouse callback registered inside the render loop with `glfwSetCursorPosCallback(gWindow, mouse_callback)` on every iteration instead of once during init. Waste of cycles, and the function pointer is already the same every time.

Camera movement doesn't use deltaTime properly. The variables are declared but the actual movement in UProcessInput just adds `cameraSpeed * cameraFront` without multiplying by deltaTime. Works on my machine at 60fps but anyone with a different refresh rate gets different movement speed.

All object transforms are hardcoded in the render function. Scale, rotation, translation matrices built with magic numbers right before each draw call. No concept of an object with position, rotation, and scale properties -- just inline matrix math repeated for each object.

## portfolio take

Archive. It demonstrates solid OpenGL fundamentals -- shaders, lighting, textures, VAOs, camera controls -- but the single-file structure and hardcoded geometry make it hard to read as anything other than a class assignment.
