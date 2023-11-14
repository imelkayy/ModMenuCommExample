# Mod Menu Documention
By elkay

## Integrating your mod
The source code within this repository contains a CCA, Buff, Function Library, and Example UI. When migrating into your own mod, make sure to ensure no files are referencing anything not within your mod directory (ie: you don't want the ExampleUI, ensure ExampleBuff isn't referencing it).

**Example UI** - A basic UI designed to showcase the UI-opening feature. It is crucial to remember to notify the Mod Menu UI when your UIs are closed.


## CCA
The CCA example is where most of the critical logic is performed. it informs the Mod Menu CCA of your settings and UIs. Setting information (everything EXCEPT the player-set value) will be reset to what is contained within your CCA.

Implements: Mod Communication Interface

### [Send Function Name]
This function sends your mod's Settings and UIs to the Mod Menu CCA for processing. Your settings are packaged into a single key, using delimters of `;` and `|` (so please do not use these anywhere within your settings!). UIs are packaged and sent to the Mod Menu CCA individually!

### Settings
All of these arrays must match lengths on your CCA, since the indicies of each array correlate to a specific setting.
- **Category:** (Name) the category your setting belongs to. Standard: ``ModName/Category``. NOTE: The category is used to sort by-mod, so this standard is critical!
- **UUID:** (Name) the Unique ID of your setting. Standard: ``ModPrefix_SettingName``
- **Type:** (Enum) the TYPE of setting that your setting is. Possible types are:
  - `String`
  - `Integer`
  - `Boolean`
  - `Float`
  - `Status Value`
  - `Vector`
- **Name:** (String) the name of the setting, displayed to the player.
- **Description:** (String) the custom description of your setting
- **Value:** (String) the DEFAULT value of your setting. Will NOT be overridden on preexisting saves if changed later.
- **MinMax:** (String[]) the minimum and maximum allowed values that can be input. Only applies to: `Integer` and `Float` types. Leave BLANK for other setting types.

## Function Library
The function library provides a function capable of grabing the value of ANY Mod Menu setting, using it's UUID.

### GetSettingValue
Returns the String value of the setting called for. For non-string settings, the String will be ready to convert to other options.
```
Input: SettingUUID (Name)
Output: Value (String)
```

## ExampleBuff
The example buff provides sample functionality on how to handle adding your UIs to viewport when their respective Mod Menu buttons have been pressed.

### Custom Tag
The ``CustomTag`` of your buff MUST be `MainBuff_[YourMod]`, where [YourMod] is the ModName used inside the CCA (for adding your UIs), without spaces.

### Adding your UI
The `HandleSendModData` function showcases how to handle receiving input to open your UI. You can implement UI opening however you like, however please ensure you notify the Mod Menu UI if you fail to open the UI for some reason (example of this can be seen in the ExampleUI).

## ExampleUI
The ExammpleUI provided is very barebones, showcasing what is needed to properly CLOSE your UI.

### Opening
Opening is handled by you, after your buff (see above) is notified by the Mod Menu UI. You should not need to enable input yourself, but should you need to you can without interferring with Mod Menu.

### Closing
When closing your UI, please ensure the example code is running so that the Mod Menu is notified and can properly reassume control of input and reenable it's `Close` button.