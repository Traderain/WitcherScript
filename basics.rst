Basic Witcher Script information sheet
===========================

If you have any previous experiences with any type of object oriented programming, you will have no issues with using wscript.
Syntax and usage is very similar to (now obsolete) UnrealScript.

Basic Types
--------------

- int - Standard 32 bit integer (value range from -2,147,483,648 to 2,147,483,647)
- String - Standard string, use quotation marks to pass values, eg. "This is a string"
- name  - Name type variable, essentially a string used for item names, tags, etc. Use apostrophes to pass values, eg. 'this is an item name'
- float- Standard float type, eg. 1.0f
- Vector - 4 variable vector (Quaternion) ordered in XYZW (for the most part you don't need to concern yourself with W value) order, eg. Vector(100, 100, 100, 1)
- EulerAngles - 3 variable rotation ordered in Pitch, Yaw, Roll order, eg. EulerAngles(0, 180, 0)
- bool - standard true/false boolean, also accepts 0 and 1 as inputs, however unlike Unreal Script does not accept Yes/No values
- Matrix - Indicates matrix variable type.
- array< X > - Indicates an array with X being the type of array, eg. array< int > being an array of integers


Class Types
--------------

Besides standard variable types, wscript also supports declaring class type variables, such as:

- CEntity - Standard entity
- CEntityTemplate - Entity template (resource type)

And much more, every scriptable class can be declared as a variable in order to be stored, get or set.
