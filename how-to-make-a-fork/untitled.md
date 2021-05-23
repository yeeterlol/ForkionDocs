---
description: A guide of how to change the colors!
---

# TabGUI and ClickGUI colors

## Changing the TabGUI and ClickGUI colors

We will be giving you a simple guide of changing the colors of TabGUI and ClickGUI! First go to the directory down below!

```
/Horion/Menu
```

After, we will be making some simple changes to ClickGUI.cpp

{% code title="ClickGUI.cpp" %}
```bash
static const MC_Color selectedModuleColor = MC_Color(30, 110, 200);
static const MC_Color selectedSettingColor1 = MC_Color(20, 100, 195);
static const MC_Color selectedSettingColor2 = MC_Color(40, 120, 205);
static const MC_Color moduleColor = MC_Color(5, 30, 50);
static const MC_Color SettingColor1 = MC_Color(10, 25, 45);
static const MC_Color SettingColor2 = MC_Color(20, 35, 55);

```
{% endcode %}

Replace the MC\_Colors \(RGB\) for what ever you like!

{% hint style="info" %}
You can use [this site](https://rgbcolorcode.com/) to find color's MC\_Colors \(RGB\) values.
{% endhint %}

{% hint style="danger" %}
Do not replace the colors over 255 since this is RGB! This will cause an error which will break your code.
{% endhint %}



## TabGUI

Here is the simple guide of how to change the colors of TabGUI! Go to the directory down below!

```bash
/Horion/Menu/TabGUI.cpp
```

We will be making some changes to the MC\_COLOR \(RGB\)!

```bash
int i = 0;
	float selectedYOffset = yOffset;
	float startYOffset = yOffset;
	for (auto it = labelList.begin(); it != labelList.end(); ++it, i++) {
		auto label = *it;
		vec4_t rectPos = vec4_t(
			xOffset - 0.5f,  // Off screen / Left border not visible
			yOffset,
			xOffset + maxLength + 4.5f,
			yOffset + textHeight);

		MC_Color color = MC_Color(200, 200, 200);

		if (selected[renderedLevel].selectedItemId == i && level >= renderedLevel) {  // We are selected
			if (renderedLevel == level) {                                             // Are we actually in the menu we are drawing right now?
				// We are selected in the current menu
				DrawUtils::fillRectangle(rectPos, MC_Color(13, 29, 48), 1.f);
				static bool lastVal = toggleCurrentSelection;

				if (toggleCurrentSelection) {
					if (label.mod->isFlashMode()) {
						label.mod->setEnabled(true);
					} else {
						toggleCurrentSelection = false;
						label.mod->toggle();
					}
				} else if (toggleCurrentSelection != lastVal && label.mod->isFlashMode())
					label.mod->setEnabled(false);
				lastVal = toggleCurrentSelection;
			} else {  // selected, but not what the user is interacting with
				DrawUtils::fillRectangle(rectPos, MC_Color(13, 29, 48), 1.f);
			}
			//selectedYOffset = yOffset;
		} else {  // We are not selected
			DrawUtils::fillRectangle(rectPos, MC_Color(13, 29, 48), 1.f);
		}

		std::string tempLabel(label.text);
		DrawUtils::drawText(vec2_t(xOffset + 1.5f, yOffset + 0.5f), &tempLabel, label.enabled ? MC_Color() : color, textSize);
```



Replace any changes with MC\_Color and it should work!

