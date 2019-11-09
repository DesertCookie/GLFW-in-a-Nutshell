---
description: Preparing the library for use
---

# Library Setup

## Import

Speaks for itself, I think...

{% tabs %}
{% tab title="Java" %}

```java
import static org.lwjgl.glfw.GLFW.*;
```

{% endtab %}
{% tab title="C++" %}

```cpp
#include <GLFW/glfw3.h>
```

{% endtab %}
{% tab title="C" %}

TODO

{% endtab %}
{% endtabs %}

## Initialization

Before most GLFW functions may be called, the library must be initialized. This initialization process can fail, which should to be accounted for:

{% tabs %}
{% tab title="Java" %}

```java
if(!glfwInit())
    throw new RuntimeException("Failed to initialize GLFW");
```

{% endtab %}
{% tab title="C++" %}

```cpp
if(!glfwInit()) {
    std::cout << "Failed to initialize GLFW" << std::endl;
    return -1;
}
```

{% endtab %}
{% tab title="C" %}

```c
if (!glfwInit()) {
    fprintf(stderr, "Failed to initialize GLFW\n");
    return -1;
}
```

{% endtab %}
{% endtabs %}

There are a few functions that may be called before GLFW is successfully initialized:

* `glfwGetVersion`
* `glfwGetVersionString`
* `glfwGetError`
* `glfwSetErrorCallback`
* `glfwInitHint`
* `glfwTerminate`

## Termination

Before an application exits, the library must be terminated using `glfwTerminate()`, to prevent memory leaks. This will also [destroy all existing windows], [monitors](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/monitors/monitor-basics#querying-monitors) and [cursors](https://app.gitbook.com/@desertcookie/s/glfw-in-a-nutshell/input/mouse#custom-cursors).

## Error Handling

Even before initializing GLFW, an error callback can be set that can be used to print errors directly to console:

{% tabs %}
{% tab title="Java" %}

```java
GLFW.glfwSetErrorCallback((error, description) -> {
    String errorDescription = MemoryUtil.memUTF8(description);
    // ...
});
```

An easier alternative:

```java
GLFWErrorCallback.createPrint(System.err).set();
```

{% endtab %}
{% tab title="C++" %}

TODO

{% endtab %}
{% tab title="C" %}

TODO

{% endtab %}
{% endtabs %}

Note: This callback later has to be freed to prevent memory leaks:

{% tabs %}
{% tab title="Java" %}

```java
glfwSetErrorCallback(null).free();
```

{% endtab %}
{% tab title="C++" %}

TODO

{% endtab %}
{% tab title="C" %}

TODO

{% endtab %}
{% endtabs %}

GLFW also caches the last error to have occurred. This error's code and optionally its description (nullable) can be queried like this: 

{% tabs %}
{% tab title="Java" %}

```java
PointerBuffer pDescription = MemoryUtil.memAllocPointer(1);
GLFW.glfwGetError(pDescription);
long pointerAddress = pDescription.get(0);
String errorDescription = MemoryUtil.memUTF8(pointerAddress);
// ...
```

{% endtab %}
{% tab title="C++" %}

```cpp
const char* description;
int code = glfwGetError(&description);
// ...
```

{% endtab %}
{% tab title="C" %}

```c
const char* description;
int code = glfwGetError(&description);
/* ... */
```

{% endtab %}
{% endtabs %}

The returned code is one of:

* `GLFW_NO_ERROR` - No error has occurred.
* `GLFW_NOT_INITIALIZED` - GLFW has not been initialized.
* `GLFW_NO_CURRENT_CONTEXT` - No context is current for this thread.
* `GLFW_INVALID_ENUM` - 	One of the arguments to the function was an invalid enum value.
* `GLFW_INVALID_VALUE` - One of the arguments to the function was an invalid value.
* `GLFW_OUT_OF_MEMORY` - 	A memory allocation failed.
* `GLFW_API_UNAVAILABLE` - GLFW could not find support for the requested API on the system.
* `GLFW_VERSION_UNAVAILABLE` - The requested OpenGL or OpenGL ES version is not available.
* `GLFW_PLATFORM_ERROR` - A platform-specific error occurred that does not match any of the more specific categories.
* `GLFW_FORMAT_UNAVAILABLE` - The requested format is not supported or available.
* `GLFW_NO_WINDOW_CONTEXT` - The specified window does not have an OpenGL or OpenGL ES context.

## Initialization Hints

Before initialization of GLFW, initialization hints can be used to set up specific library behaviors.  

|            Hint            | Default value |                                       Explanation                                       |
| -------------------------- | ------------- | --------------------------------------------------------------------------------------- |
| GLFW_JOYSTICK_HAT_BUTTONS  | GLFW_TRUE     | Whether to expose joystick hats as button for GLFW backward compatibility.              |
| GLFW_COCOA_CHDIR_RESOURCES | GLFW_TRUE     | *macOS-specific*. Whether to set set the application directory to `Contents/Resources`. |
| GLFW_COCOA_MENUBAR         | GLFW_TRUE     | *macOS-specific*. Whether to create a basic menu bar, when the first window is created. |

Initialization hints can be specified with `glfwInitHint(<hint>,<value>)`, where `<hint>` is one of the above, and `<value>` is one of `GLFW_TRUE`/`GLFW_FALSE`:

