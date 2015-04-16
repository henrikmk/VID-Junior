# Actors

Actors are responsible for making faces do things at particular events. For example, when pressing a button, an ```ON-LEFT-MOUSE``` function would be run.

All required actors are stored per face in the ACTOR word for the face object.

Not all actors are needed, and those are simply set to NONE.

There is no limitation to what kind of actors can be used, but any extension of the actors should be applied to the central actor object.

## Using Actors in Layout

In VID, there was an action block which was tied to the main action of the face, which would depend on the face type. For button, it would be a left mouse click. For field, it would be the Return or Enter key. Here, we will tie actions to specific actors, so there is no longer a "generic actor". Therefore, we can't just use a generic action block. It must be prefaced with the name of the actor:

```rebol
layout [
  button "My Button" on-left-click [perform-this-action]
]
```

## Applying Actors to Faces

Changing actors can be done with ```INSERT-ACTOR-FUNC``` and ```REMOVE-ACTOR-FUNC```.

Inserting the first function:

```insert-actor-func my-face 'on-left-click my-function```

It's possible to insert more functions after the first one:

```insert-actor-func my-face 'on-left-click my-function2```

The refinement ```/FROM``` can be used to grab actor functions from another face.

```insert-actor-func/from inner-face 'on-left-click my-function2 outer-face```

Removing, just requires passing the function that was inserted, and the function will be removed again:

```remove-actor-func my-face 'on-left-click my-function```

```PASS-ACTOR``` will pass actors between faces. This is useful to let a face accept an actor, and then let that be passed inwards to faces inside it, for example for a table which needs to have its scroller react to the same actor as the list.

The actor function that is run, when an actor is run takes 4 arguments:

|Word|Description|
|----|-----------|
|FACE|The face that runs the actor.|
|VALUE|The value that is returned when using GET-FACE on the face.|
|EVENT|The event that occurred, when the actor was run or NONE.|
|ACTOR|The actor being run. The function itself doesn't know where its attached.|

## Actor Object Functions

Each actor is a function that is called with the face itself as an argument. It can also be a block of functions that are performed in order.

For blocks of functions, a style can implement a set of standard actors, which then are extended by the user.

The face function ```ACT-FACE``` will perform an actor function for a specific face:

```rebol
act-face my-face 'on-left-button
```

## Actor Object

The Actor Object is simply a list of either NONE, functions or blocks of functions that run for the face they are asked to run for.

|Word|Description|Notes|
|----|-----------|-----|
|ON-LEFT-CLICK|When the left mouse button is clicked and then released over the face.|
|ON-RIGHT-CLICK|When the right mouse button is clicked and then released over the face.|
|ON-MIDDLE-CLICK|When the right mouse button is clicked and then released over the face.|
|ON-LEFT-MOUSE-DOWN|When the left mouse button is pressed down over the face.|
|ON-LEFT-MOUSE-UP|When the left mouse button is released over the face.|
|ON-MIDDLE-MOUSE|When the middle mouse button is pressed down over the face.|
|ON-RIGHT-MOUSE-DOWN|When the left mouse button is released down over the face.|
|ON-MOUSE-SCROLL|When scrolling the mouse wheel one step up or down.|
|ON-DRAG|When the left or right mouse button is pressed down and then moving the mouse.|
|ON-FACE-LEAVE|When the mouse leaves the face area.|
|ON-FACE-ENTER|When the mouse enters the face area.|
|ON-HOVER|When the mouse is hovering over the face.|This would be performed per mouse move, so should be used sparingly.|
|ON-FOCUS|When focus is set for the face.|
|ON-UNFOCUS|When focus leaves the face.|
|ON-REDRAW|When the face is redrawn.|
|ON-TIMER|When the timer event is received for the face.|
|ON-KEY|When a key is pressed for the face, if it's in focus.|
|ON-ENTER|When the Enter or Return key is pressed for the face, if it's in focus.|
|ON-ESCAPE|When pressing the Escape key for the face, if it's in focus.|
|ON-VALIDATE|When validating the face with VALIDATE-FACE.|
|ON-SHOW|When the face is displayed.|
|ON-HIDE|When the face is hidden.|
|ON-ALIGN|When the face is being aligned by the resizing system.|
|ON-RESIZE|When the face is being resized by the resizing system.|
|ON-INIT|When the face is being initialized.|Performed after initialization has completed.|
|ON-SET|When a value is being set in the face with SET-FACE.|
|ON-RESET|When the face is being reset with RESET-FACE.|
|ON-CLEAR|When the face is being cleared with CLEAR-FACE.|
|ON-SETUP|When the face is being set up with SETUP-FACE.|
|ON-POPUP|When the face generates a popup, using POPUP-FACE.|
|ON-EDIT-MODE|When the face enters or exits edit mode.|FACE/EDIT-MODE? will be set correctly, when the actor is called, and so can be used to determine, if the face has entered or exited this mode.|
|ON-EDIT-MOVE|When the face moves during edit mode.|
|ON-EDIT-RESIZE|When the face resizes during edit mode.|
|ON-RELOCATE|When the face has been relocated in the face tree with RELOCATE-FACE.|
|ON-SCREEN-ROTATE|When the screen changes orientation.|For phone/tablet interfaces.|
|ON-ACTOR|When an actor is performed (except this one).|This can be useful for debugging.|
|ON-WINDOW-OPEN|When the face that is the window face, is opened.|
|ON-WINDOW-CLOSE|When the face that is the window face, is closed.|
