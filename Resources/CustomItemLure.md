# Making a custom item with Lure

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
