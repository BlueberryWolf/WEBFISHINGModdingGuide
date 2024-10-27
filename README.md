# Webfishing Modding Guide

This guide will walk you through the entire process of decompiling the game Webfishing, setting up a modding environment exporting your mod, and using it in-game!

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
2. **EXTRACT** GodotSteam `win64-g353-s159-gs325.zip` and open that folder
3. Create a new text file titled `steam_appid.txt`
4. Open the newly created `steam_appid.txt` in notepad or your favourite text editor, and set the contents to only `3146520`, then save it.

![image](https://github.com/user-attachments/assets/45b168cc-b447-4db8-bc15-5c6ead1b4fbd)

![image](https://github.com/user-attachments/assets/4739c706-6c6f-44b3-9f9e-5ec945826524)

5. Open `godotsteam.353.editor.windows.64.exe` to open the GodotSteam editor
6. Create a new project specifically for your mod
![image](https://github.com/user-attachments/assets/dad569f6-508c-452b-a368-6f726e8ef83b)

7. Once you've created your new mod, right click on `res://` and click `Open in File Manager`

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

![image](https://github.com/user-attachments/assets/80113fda-b6f3-4ab3-8f64-b05b28161288)

      
Now, whenever you edit your mod's files inside of the Decompiled Godot project, the changes will sync to your empty project, this will save you a LOT of trouble later.

You can now close your mod's GodotSteam project by simply exiting GodotSteam.

### 4. Load the Game in GodotSteam

1. Open the decompiled Webfishing project that you've just exported in GodotSteam.
2. Ensure that there is a "mods" folder in the File Manager. If not, ensure that you've followed Step 2 properly.

![image](https://github.com/user-attachments/assets/97ed4320-4815-4c8f-b66e-f57e254deb91)

3. You can now load the game by pressing F5!

# 5. Make your mod!
### Here are some resources for making a mod
### DO NOT, I REPEAT, DO NOT, modify the game's built in code in your mod. If you need to do that, try to find another way. Otherwise, you need to use C#, you cannot do this with this guide. C# patching is for more advanced mods. I will make a C# patching guide later

For any mods that interact with the player, use my [PlayerAPI]():
* Use cases: Accessing a player when they join, editing properties of a player, getting a player by their steam ID, getting a list of players in the game
* Example: [Making a mod that modifies the player's walk_speed using the PlayerAPI](/resources/PlayerAPI.md)

For any mods that add content to the game, use [Lure](https://github.com/Sulayre/WebfishingLure)
* Custom fish, props, bobbers, colors, titles, eyes, mouths, noses, shirts/undershirts, hats, accessories, species, voices, patterns, items
* Example [Making a mod that adds a custom item using Lure](/resources/Lure.md)

For any mods that register keybinds, use my [Keybinds API](https://github.com/BlueberryWolf/APIs#keybindsapi)
* Use Cases: Any mods that require a user to press a button on their keyboard, allowing the user to configure those keybinds in the settings
* Example [Registering a keybind that can be modified in the Settings](/resources/KeybindsAPI.md)

For a simple mod setup that modifies the PlayerData, follow this example guide:
* Use Cases: Basic Mod example, modifying the PlayerData (money, save data (BE CAREFUL), voice pitch, voice speed, max bait, rod luck, rod speed, etc)
* Example: [Basic mod that modifies the player's data](/resources/PlayerData.md)

To learn more about Godot 3.5.3 and how it works before making a mod, follow this guide:
* Use cases: everything. You can make basic mods by following and referencing the guide, but this will help a lot along the way
* Link: [Godot Basics for Mod Development](/resources/Godot.md)

### 6. Testing Your Mod in GodotSteam

Godot itself does not support mod loading like GDWeave does by default. To test your mod within GodotSteam:

1. Go to `Project > Project Settings` in the top menu.

![image](https://github.com/user-attachments/assets/58ef412f-688c-4ba1-8dda-ae8abc952d9f)


2. Select the `AutoLoad` tab.
3. Under "Path," click the folder icon, and select your `main.gd` file within `mods/authorname.modname/main.gd`.
4. Under "Name," name it with your mod name `AuthorName.ModName`, but remove the dot here!
   - This setup allows GodotSteam to load your mod within the decompiled project. This works by creating a new node in "/root/AuthorName.ModName" with your main.gd script attached to it, simulating how GDWeave loads your mod in game.
5. Once you've done all of this, click Add,

![image](https://github.com/user-attachments/assets/6ab452a9-b18d-43ec-b7e6-5603e05689b6)

The next instructions are entirely optional, but make development and finding errors in your mods MUCH EASIER by removing the game's built in print spam!!

6. Make sure you're in the "Script" tab at the top middle of the screen

7. Press Ctrl+Shift+R (CMD+Shift+R on Mac) to open find and replace

8. Set Find: to `print(` and set Replace: to `pass #print#(`

![image](https://github.com/user-attachments/assets/2e9a3990-9c3f-4fed-a030-b93260f48c87)

9. Click `Replace...`, then click `Replace All (NO UNDO)`  

Now, if you `print("anything to the console")` or get any errors, you can find them in the output section at the very bottom of your screen

You can click `Clear` on the output to clear the output at any point

![image](https://github.com/user-attachments/assets/810f567a-234f-425d-89e6-eead0f8034bb)


**You can now press `F5` to launch Webfishing in the engine and test/debug your mod.**

**If you did everything correctly, the game should launch and start normally!**

### 7. Exporting Your Mod

1. Close your Decompiled Webfishing project, and open GodotSteam Editor again to open your mod's **own GodotSteam project you created in Section 2 Step 6**
2. Create a brand new folder inside of `WEBFISHING/GDWeave/Mods` (your steam installation folder of WEBFISHING) called `authorname.modname`
3. Go to `Project > Export`.

4. If you see this at the bottom of your screen

![image](https://github.com/user-attachments/assets/4179f439-3e43-40c3-94f2-37d4503a3941)

* Click Manage Export Templates->Download & Install

5. Create a new Windows Export Template

![image](https://github.com/user-attachments/assets/56303782-919b-4470-a793-dd27de20b42d)

6. Under **Options**, disable `Runnable`.

![image](https://github.com/user-attachments/assets/cf216ecf-d8d6-426b-b54a-992bd9f3f858)

7. **If you are using any dependencies (BlueberryWolfiAPI, Lure, etc) make sure not to export those with your mod!!**
   * Do this by going to the Resources tab, and changing the export mode to `Export Selected Resources (and dependencies)
   * After which, only select your mod in `mods/` and not any dependencies/APIs!
   * ![image](https://github.com/user-attachments/assets/b429a40f-95b4-4b1b-b024-65b406f7ab02)

7. Choose **Export PCK/zip** and ensure `Export with Debug` is disabled, then save it into the folder you created in step 1.

### 8. Adding the Mod to Webfishing

1. Open the mod export folder you created for your mod earlier in `WEBFISHING/GDWeave/Mods` in Section 6, step 2.
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

Example:

![image](https://github.com/user-attachments/assets/78989e4c-2a7f-49f7-a651-6652204826e4)

![image](https://github.com/user-attachments/assets/42b92943-fb64-4a2f-8ee5-e5521bf648c1)

**You've just created your very own mod! You can now launch WEBFISHING and it will load, and you can share it with other people by sending them the folder to your mod in `WEBFISHING\GDWeave\Mods`. Isn't that amazing??**

# [Best Practices](/Resources/BestPractices.md)

The next section is for Developers to learn the best practices to implement while developing mods for GDWeave using GDScript before releasing them to the world

Make sure to follow the [Best Practices for WEBFISHING mods using GDWeave](/Resources/BestPractices.md)
