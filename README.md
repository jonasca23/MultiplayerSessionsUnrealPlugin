# MultiplayerSessionsUnrealPlugin
This plugins deliver a out of the box WPB and classes ready to host and join sessions. It uses Steam as test servers.

You can check all development commits on this repository: https://github.com/jonasca23/UnrealMultiplayerPluginDevelopment

## How to use:
### Install the plugin
Downlaod this repository and copy the plugin folder inside your project's main folder. Not inside Content, not inside anything, on project main folder level.
Close the editor and reopen it to check if you have "MultiplayerSession Content" and "MultiplayerSessions C++ Classes" folder inside your Plugins folder.

### Modify DefaultEngine.ini:
Go to your project's Config folder, open DefaultEngine.ini with any text editor and add this to the of your file:

```
[/Script/Engine.GameEngine]
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="OnlineSubsystemSteam.SteamNetDriver",DriverClassNameFallback="OnlineSubsystemUtils.IpNetDriver")

[OnlineSubsystem]
DefaultPlatformService=Steam

[OnlineSubsystemSteam]
bEnabled=true
SteamDevAppId=480
bInitServerOnClient = true

; If using Sessions
; bInitServerOnClient=true

[/Script/OnlineSubsystemSteam.SteamNetDriver]
NetConnectionClassName="OnlineSubsystemSteam.SteamNetConnection"
```

This will ensure that Steam is enabled as your default platform service and some other config

### Modify DefaultGame.ini:
In the same folder you modified DefaultEngine.ini, open DefaultGame.ini and add these lines:
```
[/Script/Engine.GameSession]
MaxPlayers = 100
```

### Install Online Subsystem Steam plugin
This should be done automatically when you import Plugin folder into your project since this plugin is a dependency to my plugin, but you may want to double check. You can read more about Online Subsystem Stema here: https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/Online/Steam/

### Regenerate your Visual Studio project files:
It may be a good idea to delete Intermediate, Binaries and Saved folders from you main project's folder. Delete Intermediate and Binaries folders from the plugin's folder as well. Right click you .uproject file and click on "Generate Visual Studio Project Files". Reopen and accept the message asking to rebuild your files. Just remember: version control always.

### Initialize WPB_Menu from your level's blueprint:
![image](https://user-images.githubusercontent.com/36892502/170892235-64c353ee-7e30-40d6-8ca2-84f6a6e2b533.png)
Crate these nodes on your main level to give the player a choise to Host or Join a room. Remember that in "Lobby Path" you should place your map's path. You can do this by right clicking your map's asset > copy file path. Substitute everything until Content for /Game/ and and remove .umap at the end of your file path and you should be fine. Example:
```
C:/Users/jonas/Documents/UnrealProjects/UnrealMPShooter/Content/Maps/Lobby.umap
Should be:
/Game/Maps/Lobby
```

### This is it!
Thanks for trying out this plugin. As I said, it's a really simpel plugin to make you start you multiplayer project asap, but you probably would need to change a lot of things to make a commercial game.

Hope it helps!
