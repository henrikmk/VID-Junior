# VID-Junior

## Introduction

VID Junior is a attempt at a GUI System for REBOL 2, REBOL 3, Red and World programming languages.

If you are familiar with REBOL, you probably already know VID and possibly how it felt like using it the first time. It was easy and fun, but it was too simple.

This GUI system can be considered an offspring of VID and to recapture that initial experience of using VID, but with the intent of making it complete and getting rid of not only the design flaws in VID, but also bring in many of the best parts of other GUI systems and also allow the use of modern features like hardware acceleration and touch.

## Why "VID Junior"

Like father, like son! It's benign and inviting, like the GUI system is meant to be. But the name can be changed later, if we stop liking it.

## Why another GUI system?

There is now so much experience building user interface systems on REBOL that we can make very smart decisions on how this GUI system should work and better be able to take it in the direction we want.

## Goals

**Visual Interface Dialect** - Make your user interfaces in a simple dialect in a few minutes.

**Resizing and aligning** - All windows will be resizable and buttons can be aligned through the dialect. Different resizing models may be allowed.

**Uniform face accessors** - Button or table, access both faces in the same way. You spend little time learning how to "talk" to the face object.

**Tight integration** - No external user interface libraries needed. Load a single .r file into REBOL 2, REBOL 3, Red or World and get going. Future versions may come integrated directly with the language, if allowed.

**Capability management** - Not all languages are created equal, so there will be a way to easily manage, when a feature is available or not. Is there OpenGL? Is there rich text? Is there touch capability? Find out quickly.

**Sensible face management** - VID creates a tree of face objects. We need all sorts of functions to manipulate, traverse, search and navigate that face tree.

**Forms** - Write usable forms in a few minutes, complete with tab navigation, validation and error handling.

**Policies** - What happens when a window opens with a form? You need to validate it, focus the right field, etc. Many things that are normally written by hand, can be fully automated by the GUI system, saving you hours of coding and debugging.

**Skins** - Use bitmaps or vector drawings to make up the user interface elements. Skin handling functions will make it possible to apply a skin on a per face basis.

**Styling** - There will be a number of style management functions. Create new styles in a VID-like manner using STYLIZE.

**Menus** - It is possible to make a sensible menu system, which dynamically renders its elements and attach them to individual faces.

**Drag & Drop** - This is exploratory, as it has not really be done well before in REBOL, but a universal drag and drop model will greatly improve many usability aspects of the whole GUI system.

**Standard dialogs** - Need a palette? Yes/no dialog? They will be there. We can create a large number of different standard dialogs, using standardized code.

**Desktops, tablets and phones** - It will be possible to use on any screen format, resolution, horizontally and vertically, when the programming language allows it.

**Complete** - many more styles than in VID. No longer frustration at missing advanced tables or proper drop lists.

**Demos** - We need a number of flashy demos that are super-easy to run. Also various tools, like help viewers can grow from this system.

**Low level separation** - Using REBOL 2 as the basic specification, the other languages must present a similar face tree renderer, window management and event system.

**Fully documented** - Unlike VID, this project must be thoroughly documented. It will also be self-documenting with help strings embedded in styles and face functions.

**Recapture the VID experience** - Easy creation of super-small GUIs will be fun again!

and last, but not least...

**Interactive GUI Editor** - the architecture will be so that a GUI editor should be easy to make. VID was centered around the dialect and everything was tied up against it. We can change the design here, so the dialect draws on face manipulation functions, which a GUI editor can do too.

## Not Goals

**Not cross-platform** - The intent is *not* to, with great effort and many spent hours, make the same user interfaces run on REBOL 2 and World despite many capability differences. This is about the *experience* of using the GUI system from the view of the program writer.

**Not complex** - If a feature is too complicated, like anti-aliased rich text on REBOL 2, it will not be included, and we have already now a pretty good idea on what is possible on each programming language. That is where we take advantage of the capability model.

**No native appearance** - If a skin allows for native appearance, that is fine, but it should not be expected.
