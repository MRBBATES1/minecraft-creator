---
author: v-josjones
ms.author: v-josjones
title: How to add a Custom Block
ms.prod: gaming
description: "A tutorial that introduces a Creator on how to make a custom block within Minecraft: Bedrock Edition"
---

# How to add a Custom Block

Minecraft's behavior and resource packs allow for you to create custom content for their audience. Custom blocks are a great way for creators to start adding in interactive content that Players can interact with. Through this tutorial, you will build a new block that will be called **canvas block** that you can set up with different textures and can be placed by a Player.

:::image type="content" source="Media/CustomBlocks/Adding-a-Custom-Block.jpg" alt-text="Image of Alex holding the completed custom block":::

In this tutorial you will learn the following:

> [!div class="checklist"]
>
> - Using JSON to define a new block.
> - Assigning textures to a new block.
> - What are some of the behaviors and components that blocks can access.
> - A quick look at **.lang** and how it's used for in-game text.

### Requirements

It’s recommended that the following be completed before beginning this tutorial:

- [Getting Started with Add-On Development](GettingStarted.md)
- [Introduction To Resource Packs](ResourcePack.md)
- [Introduction To Behavior Packs](BehaviorPack.md)

You will also need the following:

- Download the [Vanilla resource pack](https://aka.ms/resourcepacktemplate)
- A Minecraft World with `Holiday Creator Features` enabled.

>[!IMPORTANT]
>Holiday Creator Features contains experimental gameplay features. As with all experiments, you may see additions, removals, and changes in functionality in Minecraft versions without significant advanced warning.
>
>To learn more about Experimental Features, please visit [Experimental Features in Minecraft: Bedrock Edition](ExperimentalFeaturesToggle.md)

## Setting up the Resource JSON File

Block entity definitions are handled differently in the resource pack. Blocks are stored in a single JSON file that will contain definitions for each custom block.

1. Open up your game location folder **com.mojang**
1. Double-click on the folder **development_resource_packs**.
1. Double-click on the folder **HelloWorldRP**.
    1. If you do not have this folder, please refer to the tutorials in the Requirements.
1. Right-click in the Explorer window and select **New**, then select **Text Document**.
1. Set the name to **blocks.json**.
1. Double-click on **blocks.json** to open it in a text editor.

### blocks.json

The blocks.json file has a similar set up to the manifest.json and has requirements in order to work correctly. The canvas block will use a custom texture for each of the size, except for the top and bottom. Those sides will be using a vanilla texture that will be brought over to the pack for use.

1. Copy/Paste the following text into your text editor.

    ```json
    {
    "format_version": "1.16.0",
      "helloworld:canvasblock": {
        "textures": {
            "up": "log_oak_top",
            "down": "log_oak_top",
            "side": "canvasblock"
            },
        "sound":"dirt"
        }
    }
    ```

1. Save the file

#### Textures and Sub-textures

As shown in the JSON code above, the canvas block is using 2 textures. The top and bottom are using the existing **log_oak_top.png** while the other side is using a custom texture. Blocks can be assigned a single texture to cover every side of a block with the same texture.

`"textures": "canvasblock"`

Textures can be broken down in to sub-texture groups. `up`, `down`, `side` are all sub-textures that allow a creator to define which face gets a certain texture. `side` can also be broken down into cardinal directions with `north`, `east`, `south` , `west`.

### terrain_texture.json

With the block defined in the **blocks.json** file, the next step is to associate the texture names with a texture file path. This is done in a terrain_texture.json file.

1. In **File Explorer**, Navigate to the folder **HelloWorldRP/textures**.
1. Right-click in the Explorer window and select **New**, then select **Text Document**.
1. Set the name to **terrain_texture.json**.
1. Double-click on **terrain_texture.json** to open it in a text editor.
1. Copy and Paste the following code:

```json
{
  "resource_pack_name": "HelloWorldBP",
  "texture_name": "atlas.terrain",
  "padding": 8,
  "num_mip_levels": 4,
  "texture_data": {
    "canvasblock": {
      "textures": "textures/blocks/canvasblock"
    },
    "log_oak_top":{
      "textures": "textures/blocks/log_oak_top"
    }
  }
}
```

6. Save the file.

### The Canvas Texture

![A PNG file that can be downloaded and used in place of a custom texture made in a photo editor](Media/CustomBlocks/canvasblock.png)

The canvas block texture will need to be created and placed in the Resource Pack.

> [!NOTE]
> The image above has been provided for the `canvasblock.png` but feel free to use a different texture.

If you are using the one provided:

1. Download the file to your computer.
1. Place `canvasblock.png` in the `HelloWorldRP/textures/blocks` folder.

If you are creating a custom one:

1. Check that the **Width** and **Height** to are set **16** each.
1. Save the file as `canvasblock.png` in the `HelloWorldRP/textures/blocks` folder.

#### Adding the log_oak_top.png

The log_oak_top.png file will also need to be added to the texture folder in the behavior pack since the `terrain_texture.json` is set to look for both textures in the HelloWorldRP folder.

1. Navigate to the `Vanilla_Resource_Pack\textures\blocks` folder and copy `log_oak_top.png`.
1. Navigate to `HelloWorldRP/textures/blocks` and paste a copy of `log_oak_top.png`.

## Setting up the Behavior JSON file

With the work in the resource pack done, the behavior pack will need to be updated with the canvas block's components.

1. In **File Explorer**, Navigate to the folder **HelloWorldBP**, located in the **development_behavior_packs** folder.
1. Right-click in the Explorer window and select **New**, then select **Folder**.
1. Set the name to **blocks**.
1. Double-click on **blocks** to open the folder.
1. Right-click in the Explorer window and select **New**, then select **Text Document**.
1. Set the name to **canvasblock.json**.
1. Double-click on **canvasblock.json** to open it in a text editor.

### Description

In the file, you will need to define what the block is, similar to the `manifest.json` file.

1. Copy and Paste the following code:

```json
{
    "format_version": "1.16.0",
    "minecraft:block": {
        "description": {
            "identifier": "helloworld:canvasblock",
            "is_experimental": false,
            "register_to_creative_menu": true
        },
```

The identifier that was used in the resource pack is defined here. The block is also set to appear in the creative menu and is not set as an experimental piece of content.

### Components

1. At the end of **CanvasBlock.json** (line 9), Copy and paste the following code:

```json
        "components": {
            "minecraft:destroy_time": 1,
            "minecraft:explosion_resistance": 5,
            "minecraft:friction": 0.6,
            "minecraft:flammable": {
                "flame_odds": 0,
                "burn_odds": 0
            },
            "minecraft:map_color": "#FFFFFF",
            "minecraft:block_light_absorption": 0,
            "minecraft:block_light_emission": 0.250
        }
    }
}
```

2. Save the file.

- **`destroy_time`** is how many player hits does it take to destroy this block.
- **`explosion_resistance`** is how resistent the block is to explosions. Higher values mean the block is less likely to break.
- **`friction`** is used to drive player and entity speeds while stepping on this block. wood and dirt are set to a friction of `0.6` while ice is set to `0.1`.
- **`flammable`** is used to contain properties on how the block handles fire events.
    - **`flame_odds`** is how likely the block is to catch fire.
    - **`burn_odds`** is how likely the block is to be destroyed when on fire.
- **`map_color`** is the color, in hex format, that is used by the map in order to symbolize the block.
- **`block_light_absorption`** is how much light the block absorbs. Value uses a range of `0` to `1` as an input.
- **`block_light_emission`** is how much light the block produces. Value uses a range of `0` to `1` as an input.

## Setting the block name with .lang

Now that both of the packs are set up and completed, the last thing is to add the name of the block using .lang.

1. In **File Explorer**, Navigate to the folder **HelloWorldRP**.
1. Right-click in the Explorer window and select **New**, then select **Folder**.
1. Set the name to **texts**.
1. Double-click on **texts** to open the folder.
1. Right-click in the Explorer window and select **New**, then select **Text Document**.
1. Set the name to **en_US.lang**
1. Double-click on **en_US.lang** to open it in a text editor.

### .lang

.lang is a file type that Minecraft uses to provide in-game text for different languages for concepts within Add-Ons. .lang files are also a convenient way to organize all custom text within an addon in a single location and also use for localizing creator content.

1. Copy and Paste the following in **en_US.lang**:
`tile.helloworld:canvasblock.name=Canvas Block`
1. Save and close.

In the code above, you are setting the name of the block to be `Canvas Block` while in-game.

### Testing the block

With the canvas block defined in both the behavior pack and resource pack, you can now test it in-game.

>[!IMPORTANT]
>You’ll also need to have a Minecraft world where cheats are enabled in order to add the block to your inventory.
>
>You will also need to have both Hello World packs enabled in the world in order to get access to the canvas block.

1. Open up the chat dialogue box (T or Enter on Windows 10 OS).
1. Type the following command: `/give @p helloworld:canvasblock`

## What's Next?

With your first custom block completed, it is recommended to view the Block JSON reference documentation to learn more about how blocks are defined within Minecraft.

> [!div class="nextstepaction"]
> [Block JSON Documentation](../Reference/Content/BlockReference/index.yml)
