---
description: The guide to make our first change
---

# Making our first change / Changing Horion text

## Changing the Horion text

We will be giving you a simple guide of changing the text on Horion! First go to the directory down below!

```
/Memory/hooks.cpp
```

{% hint style="warning" %}
If you see errors, please ignore them. This might just be issues in the code but if you want to fix it, please send a commit on GitHub. \(Visual Studio Code\)
{% endhint %}

Replace the code with your text

{% code title="hooks.cpp" %}
```bash
 					## Replace the Horion text with your client name
					static std::string name = "Client Name";
## This is the version name for builds!
					static std::string version = "Client Version";
#Dont Change anything below this.
					static std::string version = "beta";
#else
					static std::string version = "public";
#endif

					float nameLength = DrawUtils::getTextWidth(&name, nameTextSize);
					float fullTextLength = nameLength + DrawUtils::getTextWidth(&version, versionTextSize);
					vec4_t rect = vec4_t(
						windowSize.x - margin - fullTextLength - borderPadding * 2,
						windowSize.y - margin - textHeight,
						windowSize.x - margin + borderPadding,
						windowSize.y - margin);

					DrawUtils::drawRectangle(rect, MC_Color(13, 29, 48), 1.f, 2.f);
					DrawUtils::fillRectangle(rect, MC_Color(rcolors), 1.f);
					DrawUtils::drawText(vec2_t(rect.x + borderPadding, rect.y), &name, MC_Color(6, 15, 24), nameTextSize);
					DrawUtils::drawText(vec2_t(rect.x + borderPadding + nameLength, rect.w - 7), &version, MC_Color(0, 0, 0), versionTextSize);
				}
```
{% endcode %}

You will be able to have a nice custom name!

