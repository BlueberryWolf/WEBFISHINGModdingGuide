# Editing Player Properties using my PlayerAPI
This example mod prints the name of any player that joins to the console, then changes their walk_speed to 50.

**MAKE SURE to follow [the instructions]([https://github.com/BlueberryWolf/APIs](https://github.com/BlueberryWolf/APIs?tab=readme-ov-file#developer-usage-for-the-nerds)) to import my API into the project before using this example**

If you, while debugging and loaded into the world (press F5), switch to the remote scene view,

You can find the player in the editor at `/root/world/Viewport/main/entities/player`

![image](https://github.com/user-attachments/assets/f3562100-9ef8-4d7c-b5cd-c0b5ec0b994c)

Then, on the right side of the screen, (the inspector), you can find all of the properties about the player

Make sure to switch to "raw" mode

![image](https://github.com/user-attachments/assets/17d57ee8-47cd-4e18-956f-884de75fe493)

Here, you can find every internal property about the player, and they can all be changed via code!

If you use my API, you can simply write `player.` followed by the raw name of the property you wish to modify

Here's an example mod which modifies the player actor's `walk_speed` properties from a default of 3.2 to 50

You can use this mod by editing `res://mods/authorname.modname/main.gd`

![image](https://github.com/user-attachments/assets/8e0c753d-c075-406f-b324-0ba24945b879)

```gd
var PlayerAPI

func _ready():
	PlayerAPI = get_node_or_null("/root/BlueberryWolfiAPIs/PlayerAPI")
	PlayerAPI.connect("_player_added", self, "init_player")

func init_player(player: Actor):
	print("Player joined: ", PlayerAPI.get_player_name(player))
	player.walk_speed = 50
```
* **NOTE:** You can also modify PlayerData (which is in `/root/PlayerData`) in code via simply typing `PlayerData.` followed by any property you wish to modify
