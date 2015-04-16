# Face Object

The face object is the building element of the GUI. It contains all necessary information for it to be rendered by the lower layer as well as necessary structuring words for creating a face tree.

## Structure

|Word|Type|Default|Notes|
|----|:--:|:-----:|-----|
|STYLE|none! word!|none|The style name of the face, BUTTON, FIELD, etc.|
|STYLE-FLAGS|block!|[]|A block of words with face flags that cannot be changed while the face exists. They determine the nature and behavior of the face and how face functions work on it. Face functions are described in a different document.|
|FLAGS|block!|[]|A block of words with face flags that can be changed while the face exists.|
|SIZE|pair!|100x100|A negative size in X or Y can indicate that the size is not final.|
|OFFSET|pair!|0x0|The offset from the upper left corner of the face to the upper left corner of the parent face.|
|PARENT-FACE|object!|Parent face|The parent of this face. This is a mandatory value set up during layout or when moving the face to a different location. Without it, face navigation won't work.|
|PANE|none! object! block! function!|none|Description of this word in the next section|
|RESIZE-MODEL|none! word!|none|The resize model that is used to resize this face.|
|COLOR|none! tuple!|none|The background color that fills the face.|
|IMAGE|none! image!|none|An image that can be applied to the face.|
|EFFECT|none! word! block!|none|The effect or effects to be applied to the face on top of everything else.|
|DRAW|none! block!|none|The specific draw block that is used for this face. It's drawn on top of the SKIN block.|
|SKIN|none! word!|none|The skin draw block that is used for this face, referenced as a word from the skin system. The skin system is detailed in a different document.|
|FONT|none! object!|none|The font styling of the face. This is only used, if the face has text.|
|PARA|none! object!|none|The paragraph styling of the face. This is only used, when the face has text.|
|ALIGN|none! word!|none|The alignment of the face in relation to its parent face.|
|RESIZE|none! word!|none|The information that is used by the resize mechanism to correctly resize the face.|
|INIT|none! block!|none|The initial action to perform, when laying out the face.|
|TEXT|none! string! block!|none|The string to display using FONT and PARA styling objects. It can be either plain text or a rich text format dialect.|
|ACTORS|object!|actor object|An object of actor functions assigned to the face. These will be described in a separate document.|
|RATE|none! time!|none|The rate of timer events passed to the face.|
|DISABLED|logic!|false|Whether the face is disabled, i.e. cannot be interacted with, by the user.|
|SHOW?|logic!|true|Whether the face is displayed.|
|STATE|none! object!|none|The style specific state of the face. State objects can contain complex information about how to display the face, such as table headers, graph appearance, etc. and can be integrated with an undo/redo system. This object is here to avoid growing the face object itself in size for complex faces.|
|DATA|any-type!|none|The data content of the face structured in any fashion as needed.|
|DIRTY?|logic!|false|Whether the face needs to be updated.|
|ACCESS|object!|object!|An object of accessor functions, used to manipulate the behavior and content of the face. These functions are called by face functions. Accessor functions are described in a different document.|
|ID|none! binary!|none|A unique and persistent identifier for the face, which can be determined by a layout preprocessor. This is useful for automated testing.|
|RELATED|||Describes a grouping that the face may belong under.|
|EDIT-MODE?|logic!|false|Whether the face is in edit mode.|
|HELP-MODE?|none! word!|none|Whether the face is in one of several help modes. The help mode is a word.|
|ABOUT|none! string!|none|A short help string for the face style.|
|HELP|none! word! block!|none|A help word or selection block of word pairs to reference a help document, when the face is in a help mode.|
|DOC|none! word!|none|A documentation word for a style reference document.|

## PANE word

The pane can be one of four datatypes:

|Type|Description|
|----|-----------|
|none!|No face exists here.|
|object!|One face object exists here.|
|block!|A block of face objects or function!s exist here.|
|function!|The sub-faces generated are iterated faces, usually for lists. The input argument is XxY position as a pair! *More is needed here.*|

## Notable differences to VID Face Object

There is no ACTION function, as it is replaced by a function under ACTORS.

There is no EDGE word, as VID encourages styling through this word with an edge object. While it's simple, it's also inflexible, limiting the types of edges to what is possible with VIEW rather than with DRAW.

Many other words, such as for keeping text and list state are used only in a few faces, and are simply taken out. They need to be re-implemented individually for the styles that use them, and should be kept in the STATE object, to avoid mixing style specific state information with the rest of the face object.
