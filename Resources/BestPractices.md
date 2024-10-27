
# Best practices for Mod Development

### 1. AVOID PATCHING CODE UNLESS NECESSARY

Patches are very nice, because they allow you to modify the game's internal code, and directly implement your custom functionality into them.

However, if you explore the code, ask other devs for help, or explore in the Remote Scene view, you find that almost everything you want to patch can be done without patching anything

This is preferred, because patching code can easily break with a game update, but by working directly with the code in GDScript instead of modifying it, it's much easier to maintain your mods 

**Do not attempt to patch code inside of GDScript, patches to the game's internal code are made in C#** which I will make a separate guide for later, for more advanced mods

### 2. Loading Assets

If you are trying to load assets with [Lure](https://github.com/Sulayre/WebfishingLure), go to the next section.

If you want to load custom resources, create an "Assets" folder inside your mod folder

Example: `res://mods/AuthorName.ExampleMod/Assets`

Then, create any subfolders for the specific types of assets. For example: `Sounds`, `Textures`, `Cosmetics`, etc.

Then, add any asset files inside of this folder

To load assets in code, add a constant variable which **preload**s your asset at the top of your code

	* Avoid using **load** when possible, by defining your imports a the top level of your script, instead of in the _ready function

Example:

```gd
const MY_SOUND = preload("res://AuthorName.ModName/Assets/Sounds/my_sound.wav")

func _ready():
	# do something with MY_Sound
```

If you're using Lure, it loads assets differently.

### 3. Loading Assets with Lure

Lure allows you to load asset paths with 3 different prefixes:

* mod:// searches for assets starting from the folder of the mod_id you gave to the function.
* res:// searches for assets the classic way, in case you wanna search for base game assets.
* mods/<mod_id>:// searches for assets inside a specific mod's folder

Example Mod loading a cosmetic asset resource with Lure:

```gd
onready var Lure = get_node("/root/SulayreLure")

func _ready():
	Lure.add_content("AuthorName.ModName", "my_cosmetic", "mod://Assets/Cosmetics/my_cosmetic.tres", [Lure.LURE_FLAGS.FREE_UNLOCK]) 
```
