---
description: Controlling GLFW windows
---

# Actions

## Visibility

Windowed-mode windows can be hidden with `glfwHideWindow(window)` and shown with `glfwShowWindow(window)`. It is also possible to retrieve whether a window is visible, using the `GLFW_VISIBLE` [attribute](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/attributes#querying-attributes). 
By default, windows become visible instantly after [creation](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/window/window-basics#creation); this behavior can be changed using the `GLFW_VISIBLE` [creation hint](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/creation-hints#specifying-creation-hints). Showing a window, by default causes it to gain input focus, which may be changed using the `GÖFW_FOCUS_ON_SHOW` window hint.

## Closing

Closing the window from within the program can be done by calling `glfwSetWindowShouldClose(window,value)`, with `value` being one of `GLFW_TRUE` or `GLFW_FALSE`. This flag may also be set by the user clicking the close widget or using a key chord like `ALT+F4`. Checking whether the close flag has been set can be done with `glfwWindowShouldClose(window)`; this information can be used, for example, to determine whether to run the game loop or exit the application; a closed window doesn't require its [buffers to be swapped](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/window-basics#buffer-swapping-v-sync).  
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified when the close flag is set.

## Iconification

Windows can be minimized (aka. iconified) to the taskbar with `glfwIconifyWindow(window)`. This can be reversed by [restoring the window](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/actions#restoration). It is possible to retrieve whether a window is iconified, using the `GLFW_ICONIFIED` [attribute](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/attributes#querying-attributes).   
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified when a window is iconified or restored.

## Maximization

Windowed-mode windows can be maximized with `glfwMaximizeWindow(window)`. This can be reversed by [restoring the window](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/actions#restoration). It is possible to retrieve whether a window is maximized, using the `GLFW_MAXIMIZED` [attribute](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/attributes#querying-attributes). Windows can be set to immediately maximize after creation using the `GÖFW_MAXIMIZED` [creation hint](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/creation-hints#specifying-creation-hints).  
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified when a window is maximized or restored.  

## Restoration

Iconified or maximized windows may be restored with `glfwRestoreWindow(window)`.

## Input Focus

A window can be given input focus and brought to the front with `glfwFocusWindow(window)`. It is also possible to retrieve whether a window has input focus, using the `GLFW_FOCUSED` [attribute](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/attributes#querying-attributes).  
It is possible to [set up a callback](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/windows/callbacks#setting-callbacks) to get notified when a window gains or loses input focus.

## Attention Request

Requesting input focus can be quite disruptive. It often is wiser to send an attention request with `glfwRequestWindowAttention(window)` instead, to notify the user of an event. An attention request results in the window icon flashing in the taskbar (Windows) or jumping (macOS).

