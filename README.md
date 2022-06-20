# Android OpenGL ES Chams
In order to use this, the application needs to be using OpenGL ES for graphics rendering, otherwise it will not work. I will also be working on a project similar to this one, but it will provide support for applications that use Vulkan to render. I've included descriptive comments within the main header to provide easy insight on the code. In the example, I used [ARMPatch](https://github.com/RusJJ/ARMPatch/) as my hooking framework.

Forward Assault has been used as the target.

## Features
* Dump shaders to your devices /Downloads/ directory (which can be easily changed), or view shader names directly through a log. Both features use glGetUniformLocation.
* Get the location of a uniform from the current program ID and uniform name, instead of having to rely on the count to modify a specific uniform.
* Render primitives (triangles, lines, etc) using glDrawElements.

## Implementation
1. You will need to include the GLESv2 library into your project (which we get directly from the Android NDK). Depending on what you're using to build the application, the process will be a little bit different.

CMake (CMakeLists.txt):
```
find_library( # Sets the name of the path variable.

        GLESV2_LIB

        # Specifies the name of the NDK library that

        # you want CMake to locate.

        GLESv2)

target_link_libraries( # Specifies the target library.

        ${GLESV2_LIB}) 
```

NDK Build (Android.mk):
```
LOCAL_LDLIBS := -lGLESv2
```

2. You will also need to include the gl2 header (provided by the NDK) somewhere in your project. I've included it in my native-lib.cpp as seen [here](https://github.com/Rev/Android-Native-Mod-Template/blob/master/app/src/main/cpp/native-lib.cpp).
```
#include <GLES2/gl2.h>
```

3. Call isChams somewhere after you have included the provided chams header - such as in your main thread. 
```
isChams();
```

## Examples
I've included many examples of the limitless 'types' of chams that you can do. These examples can be found in the [main header](https://github.com/Rev/Android-OpenGL-ES-Chams/blob/main/Chams.h).

* Invisible Chams ![image](https://user-images.githubusercontent.com/64957743/173176435-eb201f00-ed9e-4d27-b87f-a0606006f64d.png)
* Black Flat Chams ![image](https://user-images.githubusercontent.com/64957743/173176366-04663aa3-7236-4efc-ad20-55b6138b2b3e.png)
* Wireframe Chams ![image](https://user-images.githubusercontent.com/64957743/173176396-2375e86b-9eab-4945-aae9-728a23714a07.png)
* Visibility Check Chams ![image](https://user-images.githubusercontent.com/64957743/173176411-b4c6df81-1010-4815-bc72-c66d87efcd8f.png)
* Base-Colour Chams ![image](https://user-images.githubusercontent.com/64957743/173176486-b2d18573-fa08-437d-bbff-6097b0d1b850.png)
