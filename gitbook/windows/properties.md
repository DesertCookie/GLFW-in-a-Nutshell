---
description: Getting and setting GLFW window properties
---

# Properties

## Title

A window's title can be set using `glfwSetWindowTitle(window,title)`, where `title` is a UTF-8 encoded string.  
It can be retrieved using `glfwGetWindowTitle(window)`.

## Position

The position of a windowed-mode window can be set with `glfwSetWindowPos(window,xpos,ypos)`; `xpos` and `ypos` are integer values, describing at which screen coordinates the window's upper left corner should be positioned. The position can be retrieved using `glfwGetWindowPos(window,xpos,ypos)`, where `xpos` and `ypos` are pointers to the variables you want the window position to be stored in (in Java normal variables have to be used, as there are no pointers).  
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified of positional changes.

## Size

The size of a window can be set with `glfwSetWindowSize(window,width,height)`; `width` and `height` have to be positive integer values, describing the window's size (including the titlebar, if visible) in screen coordinates. The size can be retrieved using `glfwGetWindowSize(window,width,height)`, where `width` and `height` are pointers to the variables you want the window size to be stored in (in Java normal variables have to be used).  
For [fullscreen windows](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/fullscreen), the specified values become the new resolution of the window's [video mode](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/monitors/video-modes#video-modes); if the monitor's and the window's video mode differ, window contents may be displayed stretched or in a different unpleasant to watch manner.  
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified of size changes. You may prohibit the user from manually resizing the window using the `GLFW_RESIZABLE` [creation hint](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/creation-hints#specifying-creation-hints).

To get the size of the display area for a window, excluding the titlebar and window frames, `glfwGetWindowFrameSize(window,left,top,right,bottom)` can be used. This returns the size of window decorations (if present); the size of the display subsequently can be calculated from the retrieved values. As above `left`, `right`, `top`, and `bottom` are pointers to variables; any of these parameters may be `NULL`.

## Size Limits

The minimum and maximum size of a windowed-mode window can be enforced with `glfwSetWindowSizeLimits(window,minwidth,minheight,maxwidth,maxheight)`; `minwidth`, `minheight`, `maxwidth`, and `maxheight` have to be positive integer values, describing the window limits in screen coordinates, or `GLFW_DONT_CARE` (default).  
These size limitations will not be applied until the window is resized, either by the user or by the program.

You may also want to enforce a specific aspect ratio, which you can do with `glfwSetWindowAspectRatio(window,numer,denom)`; `numer` and `denom` specify the target aspect ratio as numerator and denominator. A 16:9 aspect ratio would be enforced as follows: `glfwSetWindowAspectRatio(window,16,9)`.  
It is possible for aspect ratio and size limit to conflict, as described in the [GLFW documentation](https://glfw.org/docs/latest/group__window.html#gac314fa6cec7d2d307be9963e2709cc90).

## Framebuffer Size

A window's framebuffer size can be retrieved directly using `glfwGetFramebufferSize(window,width,height)`, or from a `GLFWFramebufferSizeCallback` (see [Callbacks](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks); `width` and `height` are again pointers, and describe the size of the window framebuffer in pixels. These values may differ from a window's size in screen coordinates, for example when the window is displayed on a high-DPI monitor.

## Content Scale

Content scale can be used to correctly scale text and UI elements, for example in high-DPI environments. The ratio between the current DPI and the platform-default DPI can be retrieved with `glfwGetWindowContentScale(window,xscale,yscale)`, where `xscale` and `yscale` are pointers to variables of type float.  
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified of scale changes. These values may change on the fly, when a system setting changes or the window is moved to a monitor with different scaling, for example.

