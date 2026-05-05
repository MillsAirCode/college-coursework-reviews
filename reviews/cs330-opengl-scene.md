# CS-330 OpenGL Scene

C++ with OpenGL 4.4, GLFW, GLEW, GLM, stb_image. A 3D scene with a textured table, book, soap, cologne bottle, and two cylinders. Two-point Phong lighting with distance attenuation. WASD + mouse camera, scroll for speed, P toggles perspective/ortho. About 1100 lines in one file.

The shader work is solid. Vertex shader does proper MVP transforms with inverse-transpose normal matrix for normals. Fragment shader loops over a Light struct array with ambient/diffuse/specular and attenuation. That's textbook Phong and I wrote it correctly. The GLSL macro for embedding shader source inline (`#define GLSL(Version, Source)`) is a trick I still think is clever for single-file projects.

The rest is a mess. One 1100-line file for everything. Vertex data for six objects is a giant float array where you calculate offsets by hand. `glGetUniformLocation` called every frame instead of cached once at init. Mouse callback registered inside the render loop on every iteration. Camera movement doesn't actually multiply by deltaTime despite declaring the variable. All transforms are magic-number matrices inline before each draw call.

I spent more time on this than most of my coursework and it shows in the shader quality. The architecture just didn't matter for the grade.

**Archive.** The shaders demonstrate real OpenGL understanding but the 1100-line monolith makes it hard to point at and say "this is how I write code."
