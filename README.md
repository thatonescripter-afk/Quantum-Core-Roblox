Quantum Core Framework
A framework for Roblox Luau to manage common game systems.

What It Is
This is a set of modules that handles graphics, audio, and UI settings from one place. It also includes a simple task scheduler to help you run code every frame without causing lag.

It's not a magic script. It just sets up the best-practice settings and gives you a clean way to organize your game's logic.

Features
RenderManager: Automatically sets graphics to Technology.Future and adds post-processing effects like Bloom, SunRays, and ColorCorrection.

AudioManager: Creates a master SoundGroup for all game audio. It adds a compressor (to make audio punchy) and a reverb (to add space).

UIManager: Fixes common UI scaling issues so your GUIs look right on all screens.

Core Scheduler: A task scheduler that runs code on the RenderStepped (client) or Heartbeat (server) events. It helps spread out heavy work over multiple frames.

File Structure The scripts need to be in this exact order to work. Place the main folder in ReplicatedStorage.

ReplicatedStorage
└── QuantumEngineCore (ModuleScript)
    ├── RenderManager (ModuleScript)
    ├── AudioManager (ModuleScript)
    └── UIManager (ModuleScript)

    How to Install
Put the QuantumEngineCore folder (with all the modules inside it) into ReplicatedStorage.

Add a LocalScript to StarterPlayer.StarterPlayerScripts.

-- In a LocalScript in StarterPlayer.StarterPlayerScripts
local QEC = require(game.ReplicatedStorage.QuantumEngineCore)
QEC.Init("Client")

Add a Script to ServerScriptService.

-- In a Script in ServerScriptService
local QEC = require(game.ReplicatedStorage.QuantumEngineCore)
QEC.Init("Server")

How to Use the Scheduler
Instead of using task.spawn() or coroutine.wrap(), you can use the built-in scheduler to run a function on the next frame. This is safer for performance.

QuantumEngineCore.ScheduleTask(context, func)
context: "Client" or "Server"

func: The function you want to run.

Example: local QEC = require(game.ReplicatedStorage.QuantumEngineCore)

local function do_heavy_work()
	print("This ran on the next frame, safely.")
	-- (your code here)
end

-- This tells the scheduler to run your function
-- on the next client-side frame.
QEC.ScheduleTask("Client", do_heavy_work)
