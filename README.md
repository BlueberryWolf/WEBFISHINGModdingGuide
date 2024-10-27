# Webfishing Modding Guide

This guide will walk you through the process of decompiling the game Webfishing and setting up a modding environment.

## Prerequisites

- **GDRE Tools**: For decompiling the game files ([Download GDRE Tools](https://github.com/bruvzg/gdsdecomp/releases/latest))
- **GodotSteam v3.25**: For running the decompiled game in Godot ([Download GodotSteam v3.25 For Windows](https://github.com/GodotSteam/GodotSteam/releases/download/v3.25/win64-g353-s159-gs325.zip))

# Development Resources

- **GodotPCKExplorer**: Allows you to view pck files without having to decompile them.This is useful because it allows you to double click on .pck files and open them easily (I recommend not to do this with webfishing.pck, but mainly to check your own mods) [Get it here](https://github.com/DmitriySalnikov/GodotPCKExplorer) 
- **My Comfy APIs**: **Makes writing mods a whole lot easier. Allows you to get the current or remote players and variables, and register keybinds which work with the in-game settings.** [USE THE APIS!!](https://github.com/BlueberryWolf/APIs)
- **Lure API**: **If you want to mod ANY fish, props, bobbers, colors, player customization, accessories, voices, patterns, items, or even maps.** [USE LURE!!](https://github.com/Sulayre/WebfishingLure).

## Steps

### 1. Decompile Webfishing

1. Download the latest version of **[GDRE Tools for Windows.](https://github.com/bruvzg/gdsdecomp/releases/latest)**
2. Locate `webfishing.pck` inside the `WEBFISHING` folder where Webfishing is installed via Steam.

![image](https://github.com/user-attachments/assets/8c0e4591-0f96-4a5f-85ad-0188d40818d6)

3. Use GDRE Tools to load the `webfishing.pck` file (do not attempt to decompile the `.exe`).
4. Do a **Full Recovery** with GDRE Tools
    - **Note**: All game code and assets are stored within `webfishing.pck`, next to the executable file.
5. Open the folder where you exported the webfishing PCK and keep it open for later! This is important later!

![image](https://github.com/user-attachments/assets/43a26111-93ae-4987-b386-18c457576c56)

This process will create a fully functional Godot project from the game files.

### 2. In GodotSteam, make a new project specifically for your mod,
1. Download **[GodotSteam v3.25 for Windows](https://github.com/GodotSteam/GodotSteam/releases/download/v3.25/win64-g353-s159-gs325.zip)**.
2. Create a new project specifically for your mod
![image](https://github.com/user-attachments/assets/dad569f6-508c-452b-a368-6f726e8ef83b)

3. Once you've created your new mod, right click on `res://` and click `Open in File Manager`

![image](https://github.com/user-attachments/assets/15caedca-95a1-4305-b48b-5ea671140937)

4. Keep this folder open for Section 3, you will thank me later!

### 3. Set Up the Mod Directory Structure

1. In the root of your Mod Project, create a new folder structure: `mods/authorname.modname`.
   - Replace `authorname` with your username.
   - Replace `modname` with the name of your mod.
2. Inside `mods/authorname.modname`, create a file called `main.gd`.
   - **Note**: GDWeave, the WEBFISHING modloader, run your `mods/authorname.modname/main.gd` file automatically, and mounts your mod in `/root/authorname.modname` (authorname.modname is specified in manifest.json of your mod).

![image](https://github.com/user-attachments/assets/41676385-fcff-43d4-a109-2c9312eaabef)

3. Ensure that both the decompiled webfishing PCK folder from earlier, and the new project folder are open!
4. Open a Command Prompt as Admin by pressing the Windows key and typing "Command Prompt" then right clicking it and running it as admin
5. Copy the following command into Command Prompt
      - Replace `webfishing` with the full path to your decompiled webfishing folder, then replace `mymod` with the full path to your new mod folder  
      ```bat
      mklink /J "webfishing/mods" "mymod/mods"
      ```
      Example:
      ```bat
      mklink /J "C:\Users\Blue\Desktop\webfishing\mods" "C:\Users\Blue\Documents\My Mods\mods"
      ```
Now, whenever you edit your mod's files inside of the Decompiled Godot project, the changes will sync to your empty project, this will save you a LOT of trouble later. 
You can now close your mod's GodotSteam project by simply exiting GodotSteam.

### 4. Load the Game in GodotSteam

1. Open the decompiled Webfishing project that you've just exported in GodotSteam.
2. Ensure that there is a "mods" folder in the File Manager. If not, ensure that you've followed Step 2 properly.

![image](https://github.com/user-attachments/assets/97ed4320-4815-4c8f-b66e-f57e254deb91)

3. Locate `SteamNetwork.gd` and open it

   ![image](https://github.com/user-attachments/assets/50edada2-b6b2-4a08-80d1-50ebe225cfcc)
   
4. Modify the `SteamNetwork.gd` file as follows:
   - Find **line 56** and change:
     ```gd
     var INIT = Steam.steamInit()
     ```
     to:
     ```gd
     var INIT = Steam.steamInit(true, 3146520)
     ```
5. You can now load the game by pressing F5!

### 5. Example mod, using my [Comfy Mod APIs](https://github.com/BlueberryWolf/APIs)
This example mod prints the name of any player that joins to the console, then changes their walk_speed to 50.

**Make sure** to follow [the instructions]([https://github.com/BlueberryWolf/APIs](https://github.com/BlueberryWolf/APIs?tab=readme-ov-file#developer-usage-for-the-nerds)) to import my API into the project before using this example

# Editing Player Properties using my PlayerAPI
**YET AGAIN, make sure to follow [the instructions]([https://github.com/BlueberryWolf/APIs](https://github.com/BlueberryWolf/APIs?tab=readme-ov-file#developer-usage-for-the-nerds)) to import my API into the project before using this example

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

### 6. Testing Your Mod in Godot

Godot itself does not support mod loading like GDWeave does by default. To test your mod within GodotSteam:

1. Go to `Project > Project Settings` in the top menu.
2. Select the `AutoLoad` tab.
3. Under "Path," choose the `main.gd` file within your mod folder.
4. Name it with your mod name.
   - This setup allows GodotSteam to load your mod within the decompiled project.

You can now press `F5` to launch Webfishing in the engine and test/debug your mod.

### 7. Exporting Your Mod

1. Open the separate project for your mod you created from earlier in GodotSteam
2. Create a brand new folder inside of `WEBFISHING/GDWeave/Mods` called `authorname.modname`
3. Go to `Project > Export` and set up a Windows export template.

![image](https://github.com/user-attachments/assets/56303782-919b-4470-a793-dd27de20b42d)

4. Under **Options**, disable `Runnable`.

![image](https://github.com/user-attachments/assets/cf216ecf-d8d6-426b-b54a-992bd9f3f858)

6. Choose **Export PCK/zip** and ensure `Export with Debug` is disabled, then save it into the folder you created in step 1.


### 8. Adding the Mod to Webfishing

1. Open the folder you created for your mod in `WEBFISHING/GDWeave/Mods` in Section 6, step 2.
2. Inside your mod's folder, create a `manifest.json` file with the following content:

   ```json
   {
     "Id": "authorname.modname",
     "PackPath": "modname.pck",
     "Dependencies": [
       "authorname.dependencyname"
     ]
   }
   ```
   - Replace `authorname` with your username.
   - Replace `modname` with the name of your mod.
**Note:** The Dependencies field can be removed if your mod does not have any dependencies.
If you're using my Comfy API, like the example project does, make sure to add my API to your manifest.json!
```json
"Dependencies": [
	"BlueberryWolfi.APIs"
]
```
You've just created your very own mod! You can now launch WEBFISHING and it will load, and you can share it with other people by sending them the folder to your mod in `WEBFISHING\GDWeave\Mods`. Isn't that amazing??
