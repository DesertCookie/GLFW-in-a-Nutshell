---
description: Creating GLFW contexts for OpenGL and OpenGL ES
---

# OpenGL \(ES\)

## Context Creation

After window creation, the created OpenGL context object needs to be made the current context by calling `glfwMakeContextCurrent(window)`. This binds the context object to the current thread. In situations where multithreading is required, a [shared context](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/contexts/context-basics#context-sharing) has to bee created. The current context can be retrieved with `glfwGetCurrentContext`, which returns the window containing the [context object](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/contexts/context-basics#context-objects).  
The first step of working with OpenGL would now be to create the OpenGL capabilities by calling `glCreateCapabilities`.

## Extensions

TODO (see [here](https://glfw.org/docs/latest/context_guide.html#context_glext) for now)

