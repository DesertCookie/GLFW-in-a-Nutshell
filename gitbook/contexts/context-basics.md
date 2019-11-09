---
description: Basics you need to know about GLFW contexts
---

# Context Basics

## Context Objects

When working with OpenGL or OpenGL ES, a GLFW window object encapsulates an OpenGL or OpenGL ES context. This context object is created when a [window is created](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/window-basics#creation) and is destroyed when a [window is destroyed](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/window-basics#destruction) or GLFW is [terminated](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/preparation/library-setup#termination). More information about working with OpenGL and OpenGL ES context can be found [here](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/contexts/opengl).

Vulkan does not require such a context object. More information about working with Vulkan can be found [here](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/contexts/vulkan).

## Creation Hints

There are a couple of [context-related window creation hints](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/creation-hints#context-related-hints) that affect context objects, for example the version or profile of OpenGL to use.

## Context Sharing

An OpenGL (ES) context object can be shared between windows. This is useful when working with multithreading, as it makes the resources created in one context available to the context on a different thread. When [creating a window](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/window-basics#creation), instead of using `NULL`, the last parameter `share` of `glfwCreateWindow` should be a pointer to the window, which's context you want the new window's context to be shared with.  
This means, to employ multithreading, a second window has to be created. This window can be made invisible by using the `GLFW_VISIBLE` [creation hint](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/creation-hints#specifying-creation-hints).

