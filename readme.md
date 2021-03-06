# garrysmod_common

A repository of common bits for compilation projects based on Garry's Mod.

The include folder has all the required headers for building modules for Garry's Mod (LuaJIT and Garry's Mod headers) with C++.

The lib folder provides files for linking on each platform supported by Garry's Mod.

There's common code for premake on the premake folder for faster development. Include this folder or premake5.lua (including this folder runs the premake5.lua file by default).
As you can see by the filename, you need premake5.

## Warning

Do not use internal classes/structures (like the GameDepot::System class or the IGamemodeSystem::Information structure) unless you compile with **Visual Studio 2010 SP1** on **release** mode for Windows. On Linux, use **GCC** between **4.4** and **4.9**. For Mac OSX, any **Xcode (using the GCC compiler)** version *MIGHT* work as long as the **Mac OSX 10.5 SDK** is used.

## Usage

In your project's premake5.lua (or whatever you named it) you should include your local copy of this repository:

```lua
include("path/to/this/repos/local/copy")
```

You don't need to place premake5.lua on the path as said on the first section.

Example:
```lua
newoption({
	trigger = "gmcommon",
	description = "Sets the path to the garrysmod_common (https://github.com/danielga/garrysmod_common) directory",
	value = "path to garrysmod_common directory"
})

local gmcommon = _OPTIONS.gmcommon or os.getenv("GARRYSMOD_COMMON")
if gmcommon == nil then
	error("you didn't provide a path to your garrysmod_common (https://github.com/danielga/garrysmod_common) directory")
end

include(gmcommon)
```

Creates the workspace with the provided workspace_name, optional workspace_add_debug for including a debug compilation mode (default is true) and optional workspace_path for files (can also be set by premake option (--workspace=path) and by default uses the value in the config file). Must be called at least once before the next functions.
```lua
CreateWorkspace({
	name = workspace_name
	[, allow_debug = workspace_add_debug]
	[, path = workspace_path]
})
```

Creates the project for the provided state on project_serverside (it's a boolean), optional project_manual_files (allows you to add the source/header files manually through the function files and default is false) and optional project_source_path for source files path (can also be set by premake option (--source=path, beware it will be used by all projects) and by default uses the value in the config file).
```lua
CreateProject({
	serverside = project_serverside
	[, manual_files = project_manual_files]
	[, source_path = project_source_path]
})
```

Call the next functions as needed. [directory] means it's optional because you can also use premake options, environments variables or the config file in this repo.
```lua
IncludeLuaShared() -- uses this repo path
IncludeDetouring() -- uses this repo detouring submodule
IncludeScanning() -- uses this repo scanning submodule

IncludeSDKCommon([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSDKTier0([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSDKTier1([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSDKTier2([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSDKTier3([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSDKMathlib([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSDKRaytrace([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
IncludeSteamAPI([directory]) -- premake option: --sourcesdk=directory - env var: SOURCE_SDK
```

## Relevant URLs

https://github.com/ValveSoftware/source-sdk-2013
https://github.com/danielga/sourcesdk-minimal
