# Capabilities

The idea of capabilities is to make it easy for the program writer to examine what VID Junior can do with the underlying REBOL runtime. For example, REBOL 2 cannot easily do anti-aliased text with proper paragraph formatting, so it makes sense to allow the program writer to easily figure this out by examining the *capabilities object*. For this, the function ```CAPABLE-OF``` can be used.

```rebol
>> capable-of 'anti-aliased-fonts?
== false
````

This would return FALSE for REBOL 2, but TRUE for REBOL 3.

As an object, all capabilities can be examined via simple path notation, but by using a CAPABILITY function, it's possible to create standard fall-back actions for cases, where a capability asked for, does not exist. This can be useful, if you're asking for a capability with an older version of VID Junior.

## Stored Values

Each capability can be set:

* By being hard coded directly.
* At build time.
* At run time, by having it as a function.

The value stored for each capability must be TRUE or FALSE. When a function is used, it must return TRUE or FALSE.

Functions can be used to detect the presence of libraries, like OpenGL, if a style needs that, and then fail appropriately, if the library was not found.

### List of Capabilities

This will be a very incomplete list, but will be expanded as we go along:

|Capability|Description|
|----------|-----------|
|opengl?|Whether OpenGL is available.|
|anti-aliased-fonts?|Whether the platform supports anti-aliased fonts.|
|high-dpi?|Whether the display is a high DPI display, such as Apple Retina or similar.|
|colors?|Whether the display is a color display.|
|draw?|Whether VID Junior can access a vector drawing dialect. For some bare-bones platforms, this may not be directly available.|
|touch?|Whether we're running on a unit with touch display and therefore can receive touch events.|
|multi-touch?|Whether we're running on a unit with multi-touch display and therefore can receive multi-touch events.|
|accelerometer?|Whether we can receive events from an accelerometer.|
|rotation?|Whether we're using a device that supports screen rotation during normal use.|
|sound?|Whether sound is available.|
|timers?|Whether timers are supported, which is important for animation and polling.|

Some of these capabilities may be hard to answer now, but it still makes sense to have them there as placeholders until they are resolved. By then it will be a simple matter of switching the returned value from a FALSE to the correct answer.
