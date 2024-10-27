### Here are some resources for making a mod
### DO NOT, I REPEAT, DO NOT, modify the game's built in code in your mod. If you need to do that, try to find another way. Otherwise, you need to use C#, you cannot do this with this guide. C# patching is for more advanced mods. I will make a C# patching guide later

### Before following any of the complicated guides below, create a very simple test mod by following this guide:

### Basic mod guide (DO THIS FIRST, please :3):
* [Make a basic test mod to learn!](/Resources/BasicMod.md)

### For any mods that interact with the player, use my [PlayerAPI]():
* Use cases: Accessing a player when they join, editing properties of a player, getting a player by their steam ID, getting a list of players in the game
* Example: [Making a mod that modifies the player's walk_speed using the PlayerAPI](/Resources/PlayerAPI.md)

### For any mods that add content to the game, use [Lure](https://github.com/Sulayre/WebfishingLure)
* Custom fish, props, bobbers, colors, titles, eyes, mouths, noses, shirts/undershirts, hats, accessories, species, voices, patterns, items
* Example [Making a mod that adds a custom item using Lure](/Resources/Lure.md)

### For any mods that register keybinds, use my [Keybinds API](https://github.com/BlueberryWolf/APIs#keybindsapi)
* Use Cases: Any mods that require a user to press a button on their keyboard, allowing the user to configure those keybinds in the settings
* Example [Registering a keybind that can be modified in the Settings](/Resources/KeybindsAPI.md)

### For a simple mod setup that modifies the PlayerData, follow this example guide:
* Use Cases: Basic Mod example, modifying the PlayerData (money, save data (BE CAREFUL), voice pitch, voice speed, max bait, rod luck, rod speed, etc)
* Example: [Basic mod that modifies the player's data](/Resources/PlayerData.md)

### To learn more about Godot 3.5.3 and how it works before making a mod, follow this guide:
* Use cases: everything. You can make basic mods by following and referencing the guide, but this will help a lot along the way
* Link: [Godot Basics for Mod Development](/Resources/Godot.md)
