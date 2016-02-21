# Face Functions

The FACE functions are functions that apply directly to a face and possibly its sub-faces. They are used to build and maintain a face tree, which can happen by directly using the functions, by the LAYOUT dialect or possibly later via a visual editor.

These functions are a central part in making the face tree more managable, both during the creation of the face tree and during the use of the face tree.

### Face Navigation

|Function|Description|
|--------|-----------|
|FIND-FACE|Returns the pane in which a face exists at the given index.|
|FIND-RELATIVE-FACE|Returns the next face from specific criteria relative to this one.|
|NEXT-FACE|This finds and returns the next face in the face tree.|
|BACK-FACE|This finds and returns the previous face in the face tree.|
|ASCEND-FACE|Traverse through parent faces until a particular condition is met or the root face is reached.|
|TRAVERSE-FACE|This traverses the face tree from the current location until it reaches the tip face and performs an action on each face.|
|GET-LEFT-MOST-FACE|Return the subface that has the left-most position in the pane.|
|GET-RIGHT-MOST-FACE|Return the subface that has the right-most position in the pane.|
|GET-BOTTOM-MOST-FACE|Return the subface that has the bottom-most position in the pane.|
|GET-TOP-MOST-FACE|Return the subface that has the top-most position in the pane.|

## Face Topology

|Function|Description|
|--------|-----------|
|MAKE-ROOT-FACE|This creates a root face (window face) and returns it.|
|GET-ROOT-FACE|Return the root face (window face) of the passed face.|
|ADD-FACE|This adds a new face object to the face passed to it.|
|REMOVE-FACE|This removes a specific face object from the face passed to it.|
|OVER-FACE|Returns the face the mouse is hovering over.|
|WITHIN-FACE?|Returns whether a face exists inside the pane of another face.|
|SET-PARENT-FACE|This sets the parent face of the face passed to it. This is typically set during layout or during a face tree change.|
|GET-PARENT-FACE|This returns the parent face of the face passed to it.|
|GET-TIP-FACE|This returns the tip face of the face passed to it.|
|GET-DEFAULT-FACE|This returns the default face in the face tree from the face passed to it, if one exists. If none exists, NONE is returned.|
|RELOCATE-FACE|This moves the face to a different location in the face tree and will run the ON-RELOCATE actor.|

### Face Flags

|Function|Description|
|--------|-----------|
|GET-FACE-FLAG|Get a flag from a face.|
|SET-FACE-FLAG|Set one or more flags in a face.|

### Face State

|Function|Description|
|--------|-----------|
|GET-FACE-STATE|Get the state of the face.|
|SET-FACE-STATE|Set the state of the face from previously obtained state data and runs the ON-STATE actor.|
|GET-INVALID-FACE|This returns the first face in the face tree from the face passed to it, that fails validation. If none exists, NONE is returned.|
|FOCUS-FACE|This focuses the face passed to it.|
|ACT-FACE|This performs an actor in the face passed to it.|

### Face Validation

|Function|Description|
|--------|-----------|
|INIT-FACE-VALIDATION|Perform initialization of validation of the face and its subfaces.|
|VALIDATE-FACE|This performs validation on the face passed to it, by validation rules stored for the face. It runs the ON-VALIDATE actor for the face.|

### Face Aligning and Resizing

|Function|Description|
|--------|-----------|
|ALIGN-FACE|This aligns the face and all sub-faces passed to it according to their align information and runs the ON-ALIGN actor for the face.|
|SIZE-FACE|This calculates sizes of the face and all sub-faces passed to it according to their resize information.|
|REALIGN-FACE|This changes the alignment of the face passed to it and performs alignment.|
|RESIZE-FACE|This changes the size of the face passed to it and calculates new sizes and runs the ON-RESIZE actor. *not sure about this one*|

### Face Setup and Content

|Function|Description|
|--------|-----------|
|SET-FACE|This sets the data contents of the face passed to it and runs the ON-SET actor.|
|GET-FACE|This returns the data contents of the face passed to it and runs the ON-GET actor.|
|SETUP-FACE|This sets up advanced faces like tables, which have many facets, and runs the ON-SETUP actor.|
|RESET-FACE|This resets the data contents of the face to its default value and runs the ON-RESET actor.|
|CLEAR-FACE|This clears the data contents of the face passed to it and runs the ON-CLEAR actor.|
|TRUNCATE-FACE|This truncates the displayed text in the face to one line and adds an ellipsis at the end of the text. This does not truncate the stored data, in case the face text is retrieved with GET-FACE.|
|DIRTIFY-FACE|Set the face as dirty and runs the ON-DIRTIFY actor. If the face is already dirty, the actor is not run.|
|CLEAN-FACE|Cleans the face and any of its subfaces and runs the ON-CLEAN actor for each face. If the face is already clean, the ON-CLEAN actor is not run.|

### Face Behavior

|Function|Description|
|--------|-----------|
|ENABLE-FACE|This enables the face passed to it any disabled faces under it. Faces that can't be enabled/disabled are skipped, but their sub-faces may be enabled.|
|DISABLE-FACE|This disables the face passed to it and any enabled faces under it. Faces that can't be enabled/disabled are skipped, but their sub-faces may be disabled.|
|DIALECT-FACE|This generates a layout block from the passed face tree.|
|SET-FACE-MODE|When the face goes into a special mode. Runs a mode-specific actor, when entering a mode, such as ON-EDIT-MODE. Runs the ON-MODE-EXIT actor, when exiting a mode.|
|SHOW-FACE|This sets the face to be shown.|
|HIDE-FACE|This sets the face to be hidden.|
|HIGHLIGHT-FACE|This highlights the face with the highlight indication and runs the ON-HIGHLIGHT actor. If the face is already highlighted, the actor is not run.|
|UNHIGHLIGHT-FACE|This unhighlights the face and runs the ON-UNHIGHLIGHT actor. If the face is already unhighlighted, the actor is not run.|
|SET-DEFAULT-FACE|Set the face to be the default face in the layout. The previous default is then no longer default.|

### Face Querying

|Function|Description|
|--------|-----------|
|COMPOUND-FACE?|Check if the face is a compound face.|
|ITERATED-FACE?|Check if the face is an iterated face.|
|DIRTY-FACE?|Check if the face is dirty.|
|VISIBLE-FACE?|Determines if the face is visible in the window, if it's hidden or partially hidden, due to being scrolled partially or fully out of view.|
|ROOT-FACE?|Determines if the face is the root face (window face).|

### Face Debugging

|Function|Description|
|--------|-----------|
|DUMP-FACE|This dumps the face tree of the face passed to it in a console readable format.|
