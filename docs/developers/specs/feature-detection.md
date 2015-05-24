# Feature Detection

The idea of *feature detection* is to make it easy for the program writer to examine what VID Junior can do with the underlying REBOL runtime. For example, REBOL 2 cannot easily do anti-aliased text with proper paragraph formatting, so it makes sense to allow the program writer to easily figure this out by examining the *GUI feature object*. For this, the function ```GUI-SUPPORTS?``` can be used.

```rebol
>> gui-supports? 'anti-aliased-fonts
== false
````

This would return FALSE for REBOL 2, but TRUE for REBOL 3.

To detect multiple GUI features at one time, a block would be passed:

```rebol
>> gui-supports? [anti-aliased-fonts open-gl]
== true
```

To detect any gui features, the ```/ANY``` refinement could be used:

```rebol
>> gui-supports?/any [anti-aliased-fonts open-gl]
== true
```

As an object, all GUI features can be examined via simple path notation, but by using a GUI-SUPPORTS? function, it's possible to create standard fall-back actions for cases, where a desired GUI feature, does not exist. This can be useful, if you're asking for a GUI feature with an older version of VID Junior.

## Stored Values

The GUI Feature object would be stored somewhere centrally inside a VID Junior context.

A GUI feature can be marked as detected:

* By being hard coded directly.
* At build time.
* At run time, by having it as a function.

The value stored for each GUI feature must be TRUE or FALSE. When a function is used, it must return TRUE or FALSE.

Functions can be used to detect the presence of libraries, like OpenGL, if a style needs that, and then fail appropriately, if the library was not found. The function should not be run once and then replaced by a result, but on every call.

### List of GUI Features

This will be a very incomplete list, but will be expanded as we go along:

|GUI Feature|Description|
|----------|-----------|
|opengl|Whether OpenGL is available.|
|anti-aliased-fonts|Whether the platform supports anti-aliased fonts.|
|high-dpi|Whether the display is a high DPI display, such as Apple Retina or similar.|
|colors|Whether the display is a color display.|
|draw|Whether VID Junior can access a vector drawing dialect. For some bare-bones platforms, this may not be directly available.|
|touch|Whether we're running on a unit with touch display and therefore can receive touch events.|
|multi-touch|Whether we're running on a unit with multi-touch display and therefore can receive multi-touch events.|
|accelerometer|Whether we can receive events from an accelerometer.|
|rotation|Whether we're using a device that supports screen rotation during normal use.|
|sound|Whether sound is available.|
|timers|Whether timers are supported, which is important for animation and polling.|

Some of these GUI feature questions may be hard to answer now, but it still makes sense to have them there as placeholders until they are resolved, and any placeholders can be hardcoded as either TRUE or FALSE, until we can figure out how to detect them correctly.
