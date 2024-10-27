# Webfishing Modding Guide

This guide will walk you through the process of decompiling the game Webfishing and setting up a modding environment.

## Prerequisites

- **GDRE Tools**: For decompiling the game files ([Download GDRE Tools](https://github.com/bruvzg/gdsdecomp/releases/latest))
- **GodotSteam v3.25**: For running the decompiled game in Godot ([Download GodotSteam v3.25 For Windows](https://github.com/GodotSteam/GodotSteam/releases/download/v3.25/win64-g353-s159-gs325.zip))

# Development Resources

- **My Comfy APIs**: Makes writing mods a whole lot easier. Allows you to get the current or remote players and variables, and register keybinds which work with the in-game settings. [here](https://github.com/BlueberryWolf/APIs)
- **Lure API**: **If you want to mod ANY fish, props, bobbers, colors, player customization, accessories, voices, patterns, items, or even maps. [USE LURE!!](https://github.com/Sulayre/WebfishingLure).** 

## Steps

### 1. Decompile Webfishing

1. Download the latest version of **[GDRE Tools for Windows.](https://github.com/bruvzg/gdsdecomp/releases/latest)**
2. Locate `webfishing.pck` inside the `WEBFISHING` folder where Webfishing is installed via Steam.
3. Use GDRE Tools to load the `webfishing.pck` file (do not attempt to decompile the `.exe`).
4. Do a **Full Recovery** with GDRE Tools
    - **Note**: All game code and assets are stored within `webfishing.pck`, next to the executable file.

This process will create a fully functional Godot project from the game files.

### 2. Load the Game in GodotSteam

1. Download **[GodotSteam v3.25 for Windows](https://github.com/GodotSteam/GodotSteam/releases/download/v3.25/win64-g353-s159-gs325.zip)**.
2. Open the decompiled Webfishing project that you've just exported in GodotSteam.
3. Locate `SteamNetwork.gd` and open it
   ![image](https://github.com/user-attachments/assets/50edada2-b6b2-4a08-80d1-50ebe225cfcc)
   
5. Modify the `SteamNetwork.gd` file as follows:
   - Find **line 56** and change:
     ```gd
     var INIT = Steam.steamInit()
     ```
     to:
     ```gd
     var INIT = Steam.steamInit(true, 3146520)
     ```

### 3. Set Up the Mod Directory Structure

1. In the root of the decompiled project, create a new folder structure: `mods/authoorname.modname`.
   - Replace `authorname` with your username.
   - Replace `modname` with the name of your mod.
3. Inside `mods/authorname.modname`, create a script called `main.gd`.
   - **Note**: GDWeave, the modloader, loads mods from `mods/modname/main.gd`.

### 4. Example mod, using my [Comfy Mod APIs](https://github.com/BlueberryWolf/APIs)
This example mod prints the name of any player that joins to the console, then changes their walk_speed to 50.
**Make sure** to follow [the instructions]([https://github.com/BlueberryWolf/APIs](https://github.com/BlueberryWolf/APIs?tab=readme-ov-file#developer-usage-for-the-nerds)) to import my API into the project before using this example
If you, while debugging and loaded into the world (press F5), switch to the remote scene view,
You can find the player in the editor at `/root/world/Viewport/main/entities/player`

![image](https://github.com/user-attachments/assets/f3562100-9ef8-4d7c-b5cd-c0b5ec0b994c)

Then, on the right side of the screen, (the inspector), you can find all of the properties about the player
Make sure to switch to "raw" mode

![image](https://github.com/user-attachments/assets/17d57ee8-47cd-4e18-956f-884de75fe493)

Here, you can find every internal property about the player, and they can all be changed via code!
If you use my API, you can simply write `player.` followed by the raw name of the property you wish to modify

Here's an example mod which modifies the player actor's `walk_speed` properties from a default of 3.2 to 50

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

### 5. Testing Your Mod in Godot

Godot itself does not support mod loading like GDWeave does by default. To test your mod within GodotSteam:

1. Go to `Project > Project Settings` in the top menu.
2. Select the `AutoLoad` tab.
3. Under "Path," choose the `main.gd` file within your mod folder.
4. Name it with your mod name.
   - This setup allows GodotSteam to load your mod within the decompiled project.

You can now press `F5` to launch Webfishing in the engine and test/debug your mod.

### 6. Exporting Your Mod

1. Create a new Godot project specifically for your mod.
2. Copy and paste the `mods` folder (from Step 3) into this new project.
3. Go to `Project > Export` and set up a Windows export template.
4. Under **Options**, disable `Runnable`.
5. Choose **Export PCK/zip** and ensure `Export with Debug` is disabled.

### 7. Adding the Mod to Webfishing

1. Navigate to the Webfishing directory in your Steam installation.
2. In `WEBFISHING/GDWeave/Mods`, create a new folder for your mod and add your `.pck` file.
3. Inside your mod's folder, create a `manifest.json` file with the following content:

   ```json
   {
     "Id": "AuthorName.ModName",
     "PackPath": "ModName.pck",
     "Dependencies": [
       "AuthorName.DependencyName"
     ]
   }
   ```
**Note:** The Dependencies field can be removed if your mod does not have any dependencies.
