---
description: This is a guide of how to make the strafe module!
---

# Strafe

## Info

This is a tutorial of how to make the Strafe module.

## Bhop.cpp 

This is a very simple guide, we would recommend this for beginners!

{% tabs %}
{% tab title="C++" %}
{% code title="Bhop.cpp" %}
```cpp
#include "Bhop.h"

Bhop::Bhop() : IModule(0, Category::MOVEMENT, "Hop around like a bunny!") {
	registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 0.8f);
}

Bhop::~Bhop() {
}

const char* Bhop::getModuleName() {
	return ("Bhop");
}

void Bhop::onMove(C_MoveInputHandler* input) {
	auto player = g_Data.getLocalPlayer();
	if (player == nullptr) return;

	if (player->isInLava() == 1 || player->isInWater() == 1) 
		return;
	
	if (player->isSneaking()) 
		return;

	vec2_t moveVec2d = {input->forwardMovement, -input->sideMovement};
	bool pressed = moveVec2d.magnitude() > 0.01f;

	// Removing if (player->onGround && pressed)
		player->jumpFromGround();
	
	float calcYaw = (player->yaw + 90) * (PI / 180);
	vec3_t moveVec;
	float c = cos(calcYaw);
	float s = sin(calcYaw);
	moveVec2d = {moveVec2d.x * c - moveVec2d.y * s, moveVec2d.x * s + moveVec2d.y * c};
	moveVec.x = moveVec2d.x * speed;
	moveVec.y = player->velocity.y;
	moveVec.z = moveVec2d.y * speed;
	if(pressed) player->lerpMotion(moveVec);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

We will be first removing "if \(player-&gt;onGround && pressed\)" from Bhop.cpp! 



{% tabs %}
{% tab title="C++" %}
{% code title="Bhop.cpp" %}
```cpp
#include "Bhop.h"

Bhop::Bhop() : IModule(0, Category::MOVEMENT, "Hop around like a bunny!") {
	registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 0.8f);
}

Bhop::~Bhop() {
}

const char* Bhop::getModuleName() {
	return ("Bhop");
}

void Bhop::onMove(C_MoveInputHandler* input) {
	auto player = g_Data.getLocalPlayer();
	if (player == nullptr) return;

	if (player->isInLava() == 1 || player->isInWater() == 1) 
		return;
	
	if (player->isSneaking()) 
		return;

	vec2_t moveVec2d = {input->forwardMovement, -input->sideMovement};
	bool pressed = moveVec2d.magnitude() > 0.01f;

	// Removing if (player->onGround && pressed)
	// Removing player->jumpFromGround();
	
	float calcYaw = (player->yaw + 90) * (PI / 180);
	vec3_t moveVec;
	float c = cos(calcYaw);
	float s = sin(calcYaw);
	moveVec2d = {moveVec2d.x * c - moveVec2d.y * s, moveVec2d.x * s + moveVec2d.y * c};
	moveVec.x = moveVec2d.x * speed;
	moveVec.y = player->velocity.y;
	moveVec.z = moveVec2d.y * speed;
	if(pressed) player->lerpMotion(moveVec);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Our final change is that we will be removing player-&gt;jumpFromGround\(\); from the code!

## Custom strafe name \(Optional\)

This will make sure Bhop and Strafe do not interact with each other!

### Bhop.cpp

```cpp
#include "Strafe.h"

Strafe::Strafe() : IModule(0, Category::MOVEMENT, "Speedhack") {
	registerFloatSetting("Speed", &this->speed, this->speed, 0.1f, 0.8f);
}

Strafe::~Strafe() {
}

const char* Strafe::getModuleName() {
	return ("Strafe");
}

void Strafe::onMove(C_MoveInputHandler* input) {
	auto player = g_Data.getLocalPlayer();
	if (player == nullptr) return;
```

We will replace all mentions of Bhop with Strafe!

### Bhop.h

```cpp
#pragma once
#include "..\ModuleManager.h"
#include "Module.h"

class Strafe : public IModule {
private:
	float speed = 0.325f;

public:
	Strafe();
	~Strafe();

	// Inherited via IModule
	virtual const char* getModuleName() override;
	virtual void onMove(C_MoveInputHandler* input) override;
};

```

We will replace all names with Strafe again! 

{% hint style="warning" %}
Make sure to copy Bhop.h and Bhop.cpp!
{% endhint %}

We have officially finished the strafe module!

