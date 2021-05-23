---
description: 'With this guide, your fly can bypass cubecraft!'
---

# CubecraftFly

## Info

Horion already has a CubeCraft-Fly, but it is pretty outdated and old. It flags the anticheat but we will be teaching you a cubecraftfly!

### Fly.cpp

Here is a guide of how to make a custom Cubecraft Flight!

{% tabs %}
{% tab title="C++" %}
```cpp
#include "Fly.h"


```
{% endtab %}
{% endtabs %}

#### We will make sure to include Fly.h, then our next step!

{% tabs %}
{% tab title="C++" %}
```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}
```
{% endtab %}
{% endtabs %}

We will add some simple changes to register the change. We are mainly adding what category and the description of the module. We still need to make sure the modules does something when the user selects it!

{% tabs %}
{% tab title="C++" %}
```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
```
{% endtab %}
{% endtabs %}

This will make sure the ArrayList shows our Module name and registers the module

## . Finishing Touches

We will do our finishing touches for Fly.cpp, we will go into .h later

{% tabs %}
{% tab title="C++" %}
```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
void Fly::onTick(C_GameMode* gm) {
    gm->player->velocity = vec3_t(0, 0, 0); // Makes velocity to 0
}
```
{% endtab %}
{% endtabs %}

This will make sure knockback won't affect your flight by bows or items with Knockback enchantments by changing Velocity to 0.

```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
void Fly::onMove(C_MoveInputHandler* input) {
    auto player = g_Data.getLocalPlayer(); // Grabs the local player
    if (player == nullptr) return; // Checks if there is a player

```

We will be grabbing the LocalPlayer, if the player doesn't exist then the module will not work for the LocalPlayer. 

{% hint style="info" %}
The LocalPlayer is the client who is loading Minecraft. 
{% endhint %}

```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
void Fly::onMove(C_MoveInputHandler* input) {
    auto player = g_Data.getLocalPlayer(); // Grabs the local player
    if (player == nullptr) return; // Checks if there is a player
    vec2_t moveVec2d = {input->forwardMovement, -input->sideMovement}; // Input movement to the side
    bool pressed = moveVec2d.magnitude() > 0.01f; // Magitude
```

This will input our movement so the flight works. The magitude is one of the setups for the flight.

```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
void Fly::onMove(C_MoveInputHandler* input) {
    auto player = g_Data.getLocalPlayer(); // Grabs the local player
    if (player == nullptr) return; // Checks if there is a player
    vec2_t moveVec2d = {input->forwardMovement, -input->sideMovement}; // Input movement to the side
    bool pressed = moveVec2d.magnitude() > 0.01f; // Magitude
    float calcYaw = (player->yaw + 90) * (PI / 180); // Calculate where the player goes
    vec3_t moveVec; // Vector movement
    float c = cos(calcYaw); // X position movement for calculating
    float s = sin(calcYaw); // Z position movement for calculating
```

It will do vector movement and use X position and Z position to calculate where the player goes.

```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
void Fly::onMove(C_MoveInputHandler* input) {
    auto player = g_Data.getLocalPlayer(); // Grabs the local player
    if (player == nullptr) return; // Checks if there is a player
    vec2_t moveVec2d = {input->forwardMovement, -input->sideMovement}; // Input movement to the side
    bool pressed = moveVec2d.magnitude() > 0.01f; // Magitude
    float calcYaw = (player->yaw + 90) * (PI / 180); // Calculate where the player goes
    vec3_t moveVec; // Vector movement
    float c = cos(calcYaw); // X position movement for calculating
    float s = sin(calcYaw); // Z position movement for calculating
    moveVec2d = {moveVec2d.x * c - moveVec2d.y * s, moveVec2d.x * s + moveVec2d.y * c}; // sidewards / backwards extension
    moveVec.x = moveVec2d.x * speed; // Using the calculation to move at the current X position
    moveVec.y = player->velocity.y; // Using the calculation to move at the current Z position
    moveVec.z = moveVec2d.y * speed; // Using the calculation to move at the current Y position
    
```

Now the calcYaw will be used for sidewards and a backwards extension. After the calculation is done, it will move at the current X, Y, and Z position.

```cpp
#include "Fly.h"                              // Change it to whatever you like
Fly::Fly() : IModule(0x0, Category::MOVEMENT,  "Bypass cubecraft easily!" ) {
    registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 92.4f);
}

Fly::~Fly() {
}

const char* Fly::getModuleName() {
    return ("Fly");
}
bool Fly::isFlashMode() {
    return false;
}
void Fly::onMove(C_MoveInputHandler* input) {
    auto player = g_Data.getLocalPlayer(); // Grabs the local player
    if (player == nullptr) return; // Checks if there is a player
    vec2_t moveVec2d = {input->forwardMovement, -input->sideMovement}; // Input movement to the side
    bool pressed = moveVec2d.magnitude() > 0.01f; // Magitude
    float calcYaw = (player->yaw + 90) * (PI / 180); // Calculate where the player goes
    vec3_t moveVec; // Vector movement
    float c = cos(calcYaw); // X position movement for calculating
    float s = sin(calcYaw); // Z position movement for calculating
    moveVec2d = {moveVec2d.x * c - moveVec2d.y * s, moveVec2d.x * s + moveVec2d.y * c}; // sidewards / backwards extension
    moveVec.x = moveVec2d.x * speed; // Using the calculation to move at the current X position
    moveVec.y = player->velocity.y; // Using the calculation to move at the current Z position
    moveVec.z = moveVec2d.y * speed; // Using the calculation to move at the current Y position
     if (pressed) player->lerpMotion(moveVec); // Sends the movement
    C_MovePlayerPacket p(g_Data.getLocalPlayer(), *g_Data.getLocalPlayer()->getPos()); // Using the localplayer to get position and sends packets
}
```

We will now add the code which sends the movement and sends packets to get the position of the LocalPlayer. Now we are done with Fly.cpp! Let's go to Fly.h!

## Fly.h

I will be giving you a guide for Fly.h! This is a lot more simpler than you think.

```cpp
#pragma once
#include "Module.h"
```

We will include pragma and the Module.h!

{% hint style="danger" %}
Make sure your Module.h  are at \Horion\Module\Modules or it will not work! \(High chance\)
{% endhint %}

```cpp
#pragma once
#include "Module.h"

class Fly : public IModule { // Public and private
private:
```

We will be sharing 2 things, a public and a private. A private is used for special info.

```cpp
#pragma once
#include "Module.h"

class Fly : public IModule { // Public and private
private:
    float speed = 0.325f; // Set the speed to whatever you like
```

Now we added everything to the private, we will go the public. You can set the speed to whatever you like but we recommend that you should not change anything or the anticheat might detect your movements.

```cpp
#pragma once
#include "Module.h"

class Fly : public IModule {
private:
    float speed = 0.325f;

public:
    Fly();
    ~Fly();
```

We will now set our public to use Fly\(\); and ~Fly\(\);! 

```cpp
#pragma once
#include "Module.h"

class Fly : public IModule {
private:
    float speed = 0.325f;

public:
    Fly();
    ~Fly();

    virtual const char* getModuleName() override; // Checks the module name
    virtual void onTick(C_GameMode* gm) override; // Overrides gamemode
```

This will grab the module name and override the Gamemode! 

```cpp
#pragma once
#include "Module.h"

class Fly : public IModule {
private:
    float speed = 0.325f;

public:
    Fly();
    ~Fly();

    virtual const char* getModuleName() override; // Checks the module name
    virtual void onTick(C_GameMode* gm) override; // Overides gamemode 
    virtual void onMove(C_MoveInputHandler* input) override;
    virtual bool isFlashMode() override; // Checks for flashmode (Disabled)
}; 
```

This will use C\_MoveInputHandler and checks for isFlashMode\(\). We have officially done the Cubecraft Fly!

