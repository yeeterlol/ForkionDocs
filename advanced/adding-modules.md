---
description: Let's setup modules!
---

# Adding modules

## How to add them

The first step of adding modules is going to the directory down below!

```cpp
\Horion\Module\Modules
```

We will now teaching you how to make them exist in Horion's code!

## Making them exist in the code \(ModuleManager.h and ModuleManager.cpp\)

First, we will be going to ModuleManager.h in \Horion\Module

### ModuleManager.h

{% tabs %}
{% tab title="C++" %}
```cpp
#pragma once

#include <typeinfo>
#include <vector>
#include <optional>
#include <memory>
#include <mutex>
#include <shared_mutex>

#include "../../Memory/GameData.h"
// OTHER MODULES HERE (DO NOT INTERACT)
#include "Modules/ModuleName.h"
```
{% endtab %}
{% endtabs %}

You will put your module that you just added in the code! This will make sure Horion detects the code and adds the module to ClickGUI.cpp

### ModuleManager.cpp

{% tabs %}
{% tab title="C++" %}
```cpp
#include "ModuleManager.h"
#include "../../Utils/Logger.h"
#include "../../Utils/Json.hpp"

using json = nlohmann::json;

ModuleManager::ModuleManager(GameData* gameData) {
	this->gameData = gameData;
}

ModuleManager::~ModuleManager() {
	initialized = false;
	auto lock = this->lockModuleListExclusive();
	this->moduleList.clear();
}

void ModuleManager::initModules() {
	logF("Initializing modules");
	{
		auto lock = this->lockModuleListExclusive();
		// OTHER MODULES, DO NOT INTERACT!
		this->moduleList.push_back(std::shared_ptr<IModule>(new ModuleName()));
		// OTHER CODE, WE WILL NOT BE TALKING ABOUT THIS
	
```
{% endtab %}
{% endtabs %}

We are done with the first step! We will now add it to the build!

## Adding our module to the build

We will go to Horion.vcproxject and edit it via a text editor! 

```cpp
  // Do not interact
  <ItemGroup>
    <ClCompile Include="Horion\Command\CommandMgr.cpp" />
    <ClCompile Include="Horion\Command\Commands\BindCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\BruhCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\CommandBlockExploitCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ConfigCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\CoordsCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\DamageCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\DupeCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\EjectCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\EnchantCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ExecuteCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\FriendListCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\GameModeCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\GiveCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\HelpCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\HideCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ICommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ModulesCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\NameSpoofCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\NbtCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\PanicCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\PathCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\PlayerTeleportCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\RelativeTeleportCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\SayCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ScriptCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ServerCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\setoffhandCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\SetprefixCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\SpammerCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\TeleportCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\TestCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\ToggleCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\TopCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\UnbindCommand.cpp" />
    <ClCompile Include="Horion\Command\Commands\WaypointCommand.cpp" />
    <ClCompile Include="Horion\Config\AccountInformation.cpp" />
    <ClCompile Include="Horion\Config\ConfigManager.cpp" />
    <ClCompile Include="Horion\DrawUtils.cpp" />
    <ClCompile Include="Horion\FriendList\FriendList.cpp" />
    <ClCompile Include="Horion\GuiUtils.cpp" />
    <ClCompile Include="Horion\ImmediateGui.cpp" />
    <ClCompile Include="Horion\Loader.cpp" />
    <ClCompile Include="Horion\Menu\ClickGui.cpp" />
    <ClCompile Include="Horion\Menu\TabGui.cpp" />
    <ClCompile Include="Horion\Module\ModuleManager.cpp" />
    <ClCompile Include="Horion\Module\Modules\Aimbot.cpp" />
    <ClCompile Include="Horion\Module\Modules\AirJump.cpp" />
    <ClCompile Include="Horion\Module\Modules\AirStuck.cpp" />
    <ClCompile Include="Horion\Module\Modules\AirSwim.cpp" />
    <ClCompile Include="Horion\Module\Modules\AntiBot.cpp" />
    <ClCompile Include="Horion\Module\Modules\AntiImmobile.cpp" />
    <ClCompile Include="Horion\Module\Modules\AntiVoid.cpp" />
    <ClCompile Include="Horion\Module\Modules\AutoArmor.cpp" />
    <ClCompile Include="Horion\Module\Modules\AutoClicker.cpp" />
    <ClCompile Include="Horion\Module\Modules\AutoGapple.cpp" />
    <ClCompile Include="Horion\Module\Modules\AutoSneak.cpp" />
    <ClCompile Include="Horion\Module\Modules\AutoSprint.cpp" />
    <ClCompile Include="Horion\Module\Modules\AutoTotem.cpp" />
    <ClCompile Include="Horion\Module\Modules\Bhop.cpp" />
    <ClCompile Include="Horion\Module\Modules\Blink.cpp" />
    <ClCompile Include="Horion\Module\Modules\BowAimbot.cpp" />
    <ClCompile Include="Horion\Module\Modules\ChestAura.cpp" />
    <ClCompile Include="Horion\Module\Modules\ChestESP.cpp" />
    <ClCompile Include="Horion\Module\Modules\ChestStealer.cpp" />
    <ClCompile Include="Horion\Module\Modules\ClickGuiMod.cpp" />
    <ClCompile Include="Horion\Module\Modules\Compass.cpp" />
    <ClCompile Include="Horion\Module\Modules\Crasher.cpp" />
    <ClCompile Include="Horion\Module\Modules\Criticals.cpp" />
    <ClCompile Include="Horion\Module\Modules\CrystalAura.cpp" />
    <ClCompile Include="Horion\Module\Modules\CubeGlide.cpp" />
    <ClCompile Include="Horion\Module\Modules\Derp.cpp" />
    <ClCompile Include="Horion\Module\Modules\EditionFaker.cpp" />
    <ClCompile Include="Horion\Module\Modules\ESP.cpp" />
    <ClCompile Include="Horion\Module\Modules\FastEast.cpp" />
    <ClCompile Include="Horion\Module\Modules\FastLadder.cpp" />
    <ClCompile Include="Horion\Module\Modules\Fly.cpp" />
    <ClCompile Include="Horion\Module\Modules\FollowPathModule.cpp" />
    <ClCompile Include="Horion\Module\Modules\Freecam.cpp" />
    <ClCompile Include="Horion\Module\Modules\Freelook.cpp" />
    <ClCompile Include="Horion\Module\Modules\Fucker.cpp" />
    <ClCompile Include="Horion\Module\Modules\FullBright.cpp" />
    <ClCompile Include="Horion\Module\Modules\Glide.cpp" />
    <ClCompile Include="Horion\Module\Modules\Godmode.cpp" />
    <ClCompile Include="Horion\Module\Modules\HighJump.cpp" />
    <ClCompile Include="Horion\Module\Modules\Hitbox.cpp" />
    <ClCompile Include="Horion\Module\Modules\HudModule.cpp" />
    <ClCompile Include="Horion\Module\Modules\ExtendedBlockReach.cpp" />
    <ClCompile Include="Horion\Module\Modules\InfiniteReach.cpp" />
    <ClCompile Include="Horion\Module\Modules\InstaBreak.cpp" />
    <ClCompile Include="Horion\Module\Modules\InventoryCleaner.cpp" />
    <ClCompile Include="Horion\Module\Modules\InventoryMove.cpp" />
    <ClCompile Include="Horion\Module\Modules\JavascriptModule.cpp" />
    <ClCompile Include="Horion\Module\Modules\Jesus.cpp" />
    <ClCompile Include="Horion\Module\Modules\Jetpack.cpp" />
    <ClCompile Include="Horion\Module\Modules\Killaura.cpp" />
    <ClCompile Include="Horion\Module\Modules\MidClick.cpp" />
    <ClCompile Include="Horion\Module\Modules\Module.cpp" />
    <ClCompile Include="Horion\Module\Modules\NameTags.cpp" />
    <ClCompile Include="Horion\Module\Modules\Nbt.cpp" />
    <ClCompile Include="Horion\Module\Modules\NightMode.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoFall.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoFriends.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoHurtcam.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoPacket.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoPaintingCrash.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoSlowDown.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoSwing.cpp" />
    <ClCompile Include="Horion\Module\Modules\NoWeb.cpp" />
    <ClCompile Include="Horion\Module\Modules\Nuker.cpp" />
    <ClCompile Include="Horion\Module\Modules\PacketLogger.cpp" />
    <ClCompile Include="Horion\Module\Modules\Phase.cpp" />
    <ClCompile Include="Horion\Module\Modules\Radar.cpp" />
    <ClCompile Include="Horion\Module\Modules\RainbowSky.cpp" />
    <ClCompile Include="Horion\Module\Modules\Reach.cpp" />
    <ClCompile Include="Horion\Module\Modules\Scaffold.cpp" />
    <ClCompile Include="Horion\Module\Modules\Spammer.cpp" />
    <ClCompile Include="Horion\Module\Modules\Speed.cpp" />
    <ClCompile Include="Horion\Module\Modules\Spider.cpp" />
    <ClCompile Include="Horion\Module\Modules\StackableItem.cpp" />
    <ClCompile Include="Horion\Module\Modules\Step.cpp" />
    <ClCompile Include="Horion\Module\Modules\Teams.cpp" />
    <ClCompile Include="Horion\Module\Modules\Teleport.cpp" />
    <ClCompile Include="Horion\Module\Modules\TestModule.cpp" />
    <ClCompile Include="Horion\Module\Modules\Timer.cpp" />
    <ClCompile Include="Horion\Module\Modules\TimeChanger.cpp" />
    <ClCompile Include="Horion\Module\Modules\Tower.cpp" />
    <ClCompile Include="Horion\Module\Modules\Tracer.cpp" />
    <ClCompile Include="Horion\Module\Modules\TriggerBot.cpp" />
	<ClCompile Include="Horion\Module\Modules\Twerk.cpp" />
    <ClCompile Include="Horion\Module\Modules\VanillaPlus.cpp" />
    <ClCompile Include="Horion\Module\Modules\Velocity.cpp" />
    <ClCompile Include="Horion\Module\Modules\Waypoints.cpp" />
    <ClCompile Include="Horion\Module\Modules\Xray.cpp" />
    <ClCompile Include="Horion\Module\Modules\Zoom.cpp" />
    // Do not interact or errors!
    <ClCompile Include="Horion\Module\Moudles\YourModuleHere.cpp" /> // The module you want to add
  // Do not interact or errors!
 
```

We will add to the ClCompile our cpp. Now let's go to the .h!

```cpp
// DO not interact
<ItemGroup>
    // do not interact
    <ClInclude Include="Horion\Module\ModuleManager.h" />
    <ClInclude Include="Horion\Module\Modules\Aimbot.h" />
    <ClInclude Include="Horion\Module\Modules\AirJump.h" />
    <ClInclude Include="Horion\Module\Modules\AirStuck.h" />
    <ClInclude Include="Horion\Module\Modules\AirSwim.h" />
    <ClInclude Include="Horion\Module\Modules\AntiBot.h" />
    <ClInclude Include="Horion\Module\Modules\AntiImmobile.h" />
    <ClInclude Include="Horion\Module\Modules\AntiVoid.h" />
    <ClInclude Include="Horion\Module\Modules\AutoArmor.h" />
    <ClInclude Include="Horion\Module\Modules\AutoClicker.h" />
    <ClInclude Include="Horion\Module\Modules\AutoGapple.h" />
    <ClInclude Include="Horion\Module\Modules\AutoSneak.h" />
    <ClInclude Include="Horion\Module\Modules\AutoSprint.h" />
    <ClInclude Include="Horion\Module\Modules\AutoTotem.h" />
    <ClInclude Include="Horion\Module\Modules\Bhop.h" />
    <ClInclude Include="Horion\Module\Modules\Blink.h" />
    <ClInclude Include="Horion\Module\Modules\BowAimbot.h" />
    <ClInclude Include="Horion\Module\Modules\ChestAura.h" />
    <ClInclude Include="Horion\Module\Modules\ChestESP.h" />
    <ClInclude Include="Horion\Module\Modules\ChestStealer.h" />
    <ClInclude Include="Horion\Module\Modules\ClickGuiMod.h" />
    <ClInclude Include="Horion\Module\Modules\Compass.h" />
    <ClInclude Include="Horion\Module\Modules\Crasher.h" />
    <ClInclude Include="Horion\Module\Modules\Criticals.h" />
    <ClInclude Include="Horion\Module\Modules\CrystalAura.h" />
    <ClInclude Include="Horion\Module\Modules\CubeGlide.h" />
    <ClInclude Include="Horion\Module\Modules\Derp.h" />
    <ClInclude Include="Horion\Module\Modules\EditionFaker.h" />
    <ClInclude Include="Horion\Module\Modules\ESP.h" />
    <ClInclude Include="Horion\Module\Modules\FastEat.h" />
    <ClInclude Include="Horion\Module\Modules\FastLadder.h" />
    <ClInclude Include="Horion\Module\Modules\Fly.h" />
    <ClInclude Include="Horion\Module\Modules\FollowPathModule.h" />
    <ClInclude Include="Horion\Module\Modules\Freecam.h" />
    <ClInclude Include="Horion\Module\Modules\Freelook.h" />
    <ClInclude Include="Horion\Module\Modules\Fucker.h" />
    <ClInclude Include="Horion\Module\Modules\FullBright.h" />
    <ClInclude Include="Horion\Module\Modules\Glide.h" />
    <ClInclude Include="Horion\Module\Modules\Godmode.h" />
    <ClInclude Include="Horion\Module\Modules\HighJump.h" />
    <ClInclude Include="Horion\Module\Modules\Hitbox.h" />
    <ClInclude Include="Horion\Module\Modules\HudModule.h" />
    <ClInclude Include="Horion\Module\Modules\ExtendedBlockReach.h" />
    <ClInclude Include="Horion\Module\Modules\InfiniteReach.h" />
    <ClInclude Include="Horion\Module\Modules\InstaBreak.h" />
    <ClInclude Include="Horion\Module\Modules\InventoryCleaner.h" />
    <ClInclude Include="Horion\Module\Modules\InventoryMove.h" />
    <ClInclude Include="Horion\Module\Modules\JavascriptModule.h" />
    <ClInclude Include="Horion\Module\Modules\Jesus.h" />
    <ClInclude Include="Horion\Module\Modules\Jetpack.h" />
    <ClInclude Include="Horion\Module\Modules\Killaura.h" />
    <ClInclude Include="Horion\Module\Modules\MidClick.h" />
    <ClInclude Include="Horion\Module\Modules\Module.h" />
    <ClInclude Include="Horion\Module\Modules\NameTags.h" />
    <ClInclude Include="Horion\Module\Modules\Nbt.h" />
    <ClInclude Include="Horion\Module\Modules\NightMode.h" />
    <ClInclude Include="Horion\Module\Modules\NoFall.h" />
    <ClInclude Include="Horion\Module\Modules\NoFriends.h" />
    <ClInclude Include="Horion\Module\Modules\NoHurtcam.h" />
    <ClInclude Include="Horion\Module\Modules\NoPacket.h" />
    <ClInclude Include="Horion\Module\Modules\NoPaintingCrash.h" />
    <ClInclude Include="Horion\Module\Modules\NoSlowDown.h" />
    <ClInclude Include="Horion\Module\Modules\NoSwing.h" />
    <ClInclude Include="Horion\Module\Modules\NoWeb.h" />
    <ClInclude Include="Horion\Module\Modules\Nuker.h" />
    <ClInclude Include="Horion\Module\Modules\PacketLogger.h" />
    <ClInclude Include="Horion\Module\Modules\Phase.h" />
    <ClInclude Include="Horion\Module\Modules\Radar.h" />
    <ClInclude Include="Horion\Module\Modules\RainbowSky.h" />
    <ClInclude Include="Horion\Module\Modules\Reach.h" />
    <ClInclude Include="Horion\Module\Modules\Scaffold.h" />
    <ClInclude Include="Horion\Module\Modules\Spammer.h" />
    <ClInclude Include="Horion\Module\Modules\Speed.h" />
    <ClInclude Include="Horion\Module\Modules\Spider.h" />
    <ClInclude Include="Horion\Module\Modules\StackableItem.h" />
    <ClInclude Include="Horion\Module\Modules\Step.h" />
    <ClInclude Include="Horion\Module\Modules\Teams.h" />
    <ClInclude Include="Horion\Module\Modules\Teleport.h" />
    <ClInclude Include="Horion\Module\Modules\TestModule.h" />
    <ClInclude Include="Horion\Module\Modules\Timer.h" />
    <ClInclude Include="Horion\Module\Modules\TimeChanger.h" />
    <ClInclude Include="Horion\Module\Modules\Tower.h" />
    <ClInclude Include="Horion\Module\Modules\Tracer.h" />
    <ClInclude Include="Horion\Module\Modules\TriggerBot.h" />
	<ClInclude Include="Horion\Module\Modules\Twerk.h" />
    <ClInclude Include="Horion\Module\Modules\VanillaPlus.h" />
    <ClInclude Include="Horion\Module\Modules\Velocity.h" />
    <ClInclude Include="Horion\Module\Modules\Waypoints.h" />
    <ClInclude Include="Horion\Module\Modules\Xray.h" />
    <ClInclude Include="Horion\Module\Modules\Zoom.h" />
    // Do not interact or errors!
    <ClInclude Include="Horion\Module\Modules\YourModuleHere.h" /> // The module you want to edit!
    // Do not interact or errors!

```

Build your project and it should show up!

