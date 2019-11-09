---
description: Basics you should to know about GLFW windows
---

# Window Basics

## Creation

After the [GLFW initialization](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/preparation/library-setup#initialization), a GLFW window object can be created using `glfwCreateWindow(width,height,title,monitor,share)`. The parameters `monitor` (for [fullscreen windows](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/fullscreen#on-window-creation)) and `share` ([GLFW context sharing](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/fullscreen#on-window-creation)) are nullable. Window creation can fail, which should be accounted for:

{% tabs %}
{% tab title="Java" %}

```java
long window = GLFW.glfwCreateWindow(800,600,"Window",MemoryUtil.NULL,MemoryUtil.NULL);
if(window == MemoryUtil.NULL) {
	GLFW.glfwTerminate();
	throw new RuntimeException("Failed to create GLFW Window");
}
```

{% endtab %}
{% tab title="C++" %}

```cpp
GLFWwindow* window = glfwCreateWindow(800, 600, "LearnOpenGL", NULL, NULL);
if (window == NULL)
{
    std::cout << "Failed to create GLFW window" << std::endl;
    glfwTerminate();
    return -1;
}
```

{% endtab %}
{% tab title="C" %}

```c
GLFWwindow* window = glfwCreateWindow(640, 480, "Hello Triangle", NULL, NULL);
  if (!window) {
    fprintf(stderr, "Failed to create GLFW window\n");
    glfwTerminate();
    return -1;
  }
```

{% endtab %}
{% endtabs %}

If window creation was successful, an empty window will be displayed.

## Destruction

Windows and their [contexts](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/contexts/context-basics#context-objects) can be destroyed using `glfwDestroyWindow(window)`. On [termination of GLFW](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/preparation/library-setup#termination), remaining windows get destroyed automatically.

## Buffer Swapping (V-Sync)

By default, GLFW windows are double-buffered. They have a front buffer, which is displayed in the window, and a back buffer, to which is rendered. When the entire frame has been rendered, it is time to swap the back and the front buffers. This is done with `glfwSwapBuffers(window)`.  
Sometimes it is useful to have control over, when the buffer swap will occur. With the function `glfwSwapInterval(interval)` it is possible to specify the number of monitor refreshes the graphics card should wait. An `interval` of `0` swaps the buffer instantly, allowing for as high a framerate as CPU and GPU can serve. An `interval` of `1` effectively enables vertical sync (V-Sync), capping the frame rate to the monitor's refresh rate.

## Event Processing

GLFW needs to poll the operating system's window system for events. There are several functions that signal to GLFW to poll OS events:

* `glfwPollEvents` - Processes already received events and returns; best for continuous rendering.
* `glfwWaitEvents` - Waits until an event is received, then processes it.
* `glfwWaitEventsTimeout` - Waits until an event is received, or a specified time of seconds have elapsed, then processes received event(s).
* `glfwPostEmptyEvent` - Wakes the main thread if it's waiting; must be called from different thread.

Some events do not rely on being polled, e.g. the [window size callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#types-of-callbacks).

## User Pointers

Each window has a user pointer that can be set with `glfwSetWindowUserPointer(window>,<pointer)` and queried with `glfwGetWindowUserPointer(window)`. This can be used for any purpose you need and will not be modified by GLFW throughout the life-time of the window.

The initial value of the pointer is `NULL`.

