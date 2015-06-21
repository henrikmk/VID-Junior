# Compound Faces

The concept of the compound faces is a formalization of having faces grouped inside one face, for the purpose of creating one complete widget.

This has not prior been described under VID, but was described under the VID Extension Kit. The purpose of formalizing this concept is to create a convention for creating and accessing complex styles.

Under VID, this combination of faces were completely ad-hoc and different for each style. It would make it a challenge to figure out how exactly a face was put together.

An example of a compound face can be a table, and it would consist of:

* One or two scroll bars
* The table grid
* The table header

In this document, the *compound face* is the face that encompasses all other faces inside it.

Each compound face can consist of multiple other compound faces as well as sub-faces. The table header in the example above can be a compound face in itself, consisting of multiple sort-buttons.

The scroll bar would consist of the slider as a face and two arrows, each a separate face and would therefore also be a compound face.

Compound faces do not draw anything themselves. That work is relegated to sub-faces.

## What Compound Faces are Not

Compound faces are not panels with groupings of faces as specified in a layout. You can't call a loosely connected collection of fields, buttons, labels, etc. a compound face. Compound faces are defined by a style developer, not the layout developer.

They are also not faces with simple dynamic layouts, like grids or lists, as these are typically not used on their own, but are combined with scrollers and headers.

They are also not faces that work as a gateway for another displaying system, such as a 3D OpenGL view with its own internal controls and display elements.

They are also not other predefined arrangements of faces, such as forms, standard dialog layouts like palettes, search/replace dialogs or file dialogs.

A layout developer could define a layout with tightly connected faces that *appear* to be a compound face, but the developer cannot set the COMPOUND flag for the face, as this flag can only be set during style creation, as there are different kinds of flags for different situations.

## Sub-faces

The way to define sub-faces is not special: It's a face tree that is defined using a ```SETUP-FACE*``` accessor function that reads the state variables of the face to produce the necessary layout.

In VID Junior, there will be the ```ADD-FACE``` and ```REMOVE-FACE``` functions to do this.

The face tree is then places in the ```PANE``` of the compound face.

## Flags

There will be a ```COMPOUND``` flag.

**What formally declares a face as a compound face will be the ```COMPOUND``` flag.**

This flag cannot be set outside of the style creation functions, meaning, you can't set a face that has already been laid out to be a compound face.

Flags in general are described in another document.

## Access

### SET-FACE and GET-FACE

The access, such as ```SET-FACE``` and ```GET-FACE``` would use accessor functions in the compound face, to access internal values.

(How exactly the ```SET-FACE``` and ```GET-FACE``` functions work depends a lot on face traversal and the rules that apply during face traversal. This will be described in another document.)

As the compound face is special, it doesn't make sense for a table to return the header, the data, scroller state, sorting state, selection, etc. for a single ```GET-FACE``` call, as ```GET-FACE``` will normally traverse all faces inside it.

Therefore face traversal for ```GET-FACE``` should only read the compound face root, which is done by reading the ```COMPOUND``` flag, and then sub-faces are skipped.

The compound face itself can still use ```GET-FACE``` to retrieve information on faces inside itself, since its starting point for traversal isn't affected by what kind of parent faces are above it, but the same face traversal rules apply here: Any compound face inside the compound face will be treated the same way, skipping their sub-faces.

Exactly what content is returned is decided by setting a ```GET-FACE*``` access function in the compound face.

For the table, ```GET-FACE``` only reads the special information delivered by the compound face, which would be the table data. ```GET-FACE``` will recognize a compound face through the ```COMPOUND``` flag.

Other functions would be used to get/set the full state of the table.

Equally, ```SET-FACE``` will not be able to set single elements inside the table, as it can also traverse a face tree in the same way ```GET-FACE``` can.

### Accessing Sub-faces

Accessing a sub-face directly should be done via whatever access is generated from the compound-face, meaning, if for some reason, the user should be able to access the scroller directly, it's advised to make this available as a word in the compound-face, for example MY-FACE/SCROLLER. Fortunately, this is typical practice already in developing VID styles.

## Keyboard

Typically, for the keyboard to work for a particular face, the face needing keyboard events must be in focus. But for compound faces, we may need to send keyboard events to many different faces inside the face, depending on particular key presses.

So, it makes sense to have the compound face itself be in focus and then act as a relay to internal faces, for example by moving a scroller, when using the cursor keys, by calling the correct actor.

They will use ```KEY-FACE*``` accessor function to process any key events, and any faces inside them won't actually have focus, but their actors may be invoked by ```KEY-FACE*```.

Example on how to distribute key events to actors in the scroll bars ```V-SCROLLER``` and ```H-SCROLLER``` inside the compound face:

```
key-face*: func [face event] [
  switch event/key [
    up down [
      act-face face/v-scroller event 'on-key
    ]
    left right [
      act-face face/h-scroller event 'on-key
    ]
  ]
]
```

## Resizing

Since VID Junior will allow a specific resizing model per face and its sub-faces, it will be less necessary to have to write custom resizing for a compound face, but there may be cases, where it's needed anyway. When a compound face is resized with ```RESIZE-FACE```, all internal faces will be resized, using the model specified in the ```RESIZE-MODEL``` word for the compound face.

If the resize model is stated as ```CUSTOM```, the developer is expected to perform her own resizing, whenever ```RESIZE-FACE``` is called.

There will be more information regarding the different resize models in another specification document.
