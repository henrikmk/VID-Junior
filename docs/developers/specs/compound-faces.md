# Compound Styles

The concept of the compound style is just a formalization of faces grouped inside one face, for the purpose of creating one complete widget.

This has not prior been described under VID, but was described under the VID Extension Kit. The purpose of formalizing this concept is to create a convention for creating and accessing complex faces.

Under VID, this combination of faces were completely ad-hoc and different for each style. It would make it a challenge to figure out how exactly a face was put together.

An example of a compound style can be a table, and it would consist of:

* One or two scroll bars.
* The table grid
* The table header

Each compound face can consist of multiple other compound faces. The table header can be a compound face in itself, consisting of multiple sort-buttons. The scroll bar would consist of the slider as a face and two arrows, each a separate face and would therefore also be a compound face.

In this document, the *compound face* is the face that encompasses all other faces inside it.

## What They are Not

Compound faces are not panels with groupings of faces as specified in a layout. You can't call a loosely connected collection of fields, buttons, labels, etc. a compound face. Compound faces are defined by a style developer, not the layout developer.

They are also not faces with simple dynamic layouts, like grids or lists, as these are typically not used on their own, but are combined with scrollers and headers.

They are also not faces that work as a gateway for another displaying system, such as a 3D OpenGL view with its own internal controls and display elements.

A layout developer could define a layout with tightly connected faces that *appear* to be a compound face, but the developer cannot set the COMPOUND flag for the face, as this flag can only be set during style creation, as there are different kinds of flags for different situations.

## Access

The access, such as ```SET-FACE``` and ```GET-FACE``` would use accessor functions in the compound face, to access internal values.

But given that the compound face is special, it doesn't make sense for a table to return the header, the data, scroller state, sorting state, selection, etc. for a single ```GET-FACE``` call, as ```GET-FACE``` will normally traverse all faces inside it (another VID Junior design requirement).

Therefore compound faces do not allow this: ```GET-FACE``` only reads the special information delivered by the root face, which in the case of a table, would be the table data. ```GET-FACE``` will recognize a compound face through the ```COMPOUND``` flag.

The compound face itself can still use ```GET-FACE``` to retrieve information on faces inside itself.

Other functions would be used to get/set the full state of the table.

Equally, ```SET-FACE``` will not be able to set single elements inside the table, as it can also traverse a face tree in the same way ```GET-FACE``` can.

How ```SET-FACE``` and ```GET-FACE``` will work is addressed in another document.

## Sub-faces

The way to define sub-faces is not special: It's a face tree that is defined using a ```SETUP-FACE*``` accessor function that reads the state variables of the face to produce the necessary layout. The face tree is then places in the ```PANE``` of the compound face.

In VID and the VID Extension Kit, this was necessary to do with either the layout dialect or by laboriously and manually making the face tree yourself.

In VID Junior, there will be the ```ADD-FACE``` and ```REMOVE-FACE``` functions to do this as a third option, to allow dynamic rearrangements of existing face trees.

## Flags

There will be a ```COMPOUND``` flag for such faces, set when the style is created. This is useful for treating compound faces differently, when performing keyboard navigation and bringing them in and out of focus.

It is also useful for face traversal functions that gather information from forms: They know to stop when encountering a compound face and to not enter it to read every detail about it. They will only read the main compound face itself.

**What formally declares a face as a compound face will be the COMPOUND flag.**

This flag cannot, as mentioned earlier, be set outside of the style creation functions, meaning, you can't set a face that has already been laid out to be a compound face.

## Keyboard

Typically, for the keyboard to work for a particular face, the face needing keyboard events must be in focus. But for compound faces, we may need to send keyboard events to many different faces inside the face.

So, it makes sense to have the compound face act either as a relay for keyboard events to internal faces, or to convert them into meaningful actions, for example by moving a scroller, when using the cursor keys.

They will use KEY-FACE* accessor function to process any key events, and any faces inside them won't actually have focus, but their actors may be invoked by KEY-FACE*.

## Resizing

Since VID Junior will allow a specific resizing model per face and its sub-faces, it will be less necessary to have to write custom resizing for a compound face, but there may be cases, where it's needed anyway. When a compound face is resized with ```RESIZE-FACE```, all internal faces will be resized, using the model specified in the ```RESIZE-MODEL``` word for the compound face.

If the resize model is stated as CUSTOM, the developer is expected to perform her own resizing, whenever RESIZE-FACE is called.

There will be more information regarding the different resize models in another specification document.