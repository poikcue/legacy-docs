# 配置反矿物透视
*即反矿透*  
> 最初由[stonar96](https://github.com/stonar96)攥写此文并维护。    

Paper 使用基于混淆处理的反矿物透视，提供两种模式。可以对每个世界进行自定义配置。  
> **针对某个世界的配置文件**   
> 如果你还不了解Paper可以为每个世界进行自定义配置，请花上几分钟了解一下。  

本文将从头开始说明如何配置反矿物透视。有关此部分文档，请参考 每个世界的配置文件    
反矿物透视会提供两种模式。`engine-mode: 1` 将为指定维度的指定方块替换为假的方块，例如石头（y<0时为深层）、下界岩或末地岩。而 `engine-mode: 2` 与其恰好相反：将石头（y<0时为深层）、下界岩或末地岩替换为假的矿物方块。    
下图将说明启用不同模式后，开启矿物透视的玩家将会看到的图片，并且在下文会说明推荐配置。以下是主世界和下界的截图。  
![主世界](https://docs.papermc.io/assets/images/anti-xray-overworld-3443fb41851dc5d9082f2956268232a1.png)
![下界](https://docs.papermc.io/assets/images/anti-xray-nether-05e6e894ce876f94d4463e1f491d1030.png)
以客户端的角度来说，`engine-mode: 1` 模式的计算量要小很多，而 `engine-mode: 2` 模式的反矿物透视效果会更好。`engine-mode: 1` 只会隐藏周围全部被岩石包裹住的矿石，没有被包裹住的、有水的旁边的则不会隐藏。而`engine-mode: 2`不会出现以上情况，因为其工作原理是在原有原矿石的基础上额外添加假方块。

> **绕过反矿物透视**    
> **可见范围:** 即使反矿物透视可以在服务器上阻止多数玩家使用矿物透视，但不排除可能绕过的现象。通过分析反矿物透视的工作原理，玩家在服务器上可以看到他们附近大量的矿物。不过，你可以考虑再安装一个可靠的反作弊以解决此问题。不管如何，反矿物透视不是开箱即用的。  
>  **种子搜索:** 另外一种矿物透视则是根据Minecraft种子的生成规律来寻找矿物。一旦玩家得到了种子，则可以根据生成规律得知每一个矿物的位置，便能完全绕过反矿物透视。可以在Paper的配置文件中使用`feature-seeds`功能来增大玩家强行获得种子的难度，并可以和`spigot.yml`中的structure seed项配合使用。   
>  **裸露在空气中的矿石:**  在模式1和模式2中，裸露在空气中的矿石都会被开启矿物透视的玩家看到。如果开启模式2将通过增加大量的假矿石混入其中来解决这一问题。不过，开启此选项会使客户端FPS下降。  
>  **译者注:** 开启模式2后，服务器流量会大幅增加。同时，客户端（至少在开启矿物透视的情况下）将超级卡。还是建议使用模式1。

## 推荐配置
以下是启用`engine-mode: 1`和`engine-mode: 2`的不同推荐配置。  

> **代码**  
> Yaml需要注意缩进！下面的配置都正确的处理了缩进，确保在复制时正确地处理了缩进。
<!-- 这个文档居然连复制的按钮都没有。原文是“请按下右上角的复制按钮以确保正确复制缩进” -->

### `engine-mode: 1`
主世界：  
请使用以下内容来替代掉 `paper-world-defaults.yml` 中的 `anticheat.anti-xray` 键。  
```yaml
anticheat:
  anti-xray:
    enabled: true
    engine-mode: 1
    hidden-blocks:
    # 地牢中的箱子不会隐藏，因为完全裸露在空气中。但是通过藏宝图得到的宝箱则会隐藏起来。
    - chest
    - coal_ore
    - deepslate_coal_ore
    - copper_ore
    - deepslate_copper_ore
    - raw_copper_block
    - diamond_ore
    - deepslate_diamond_ore
    - emerald_ore
    - deepslate_emerald_ore
    - gold_ore
    - deepslate_gold_ore
    - iron_ore
    - deepslate_iron_ore
    - raw_iron_block
    - lapis_ore
    - deepslate_lapis_ore
    - redstone_ore
    - deepslate_redstone_ore
    lava-obscures: false
    # 1.18版本起，部分矿石的最大生成高度进行了调整。
    # 请自行修改 the max-block-height 以确保适用于当前版本。
    # https://minecraft.fandom.com/wiki/Ore 可能很有帮助
    max-block-height: 64
    replacement-blocks:
    # 调整 replacement-blocks 在使用模式1时不会生效。
    - stone
    - oak_planks
    - deepslate
    update-radius: 2
    use-permission: false
```
下界：  
复制到地狱文件夹中的`paper-world.yml`。具体请见左侧的配置文件指南。  
```yaml
anticheat:
  anti-xray:
    hidden-blocks:
    - ancient_debris
    - nether_gold_ore
    - nether_quartz_ore
    max-block-height: 128
```

末地：  
复制到末地文件夹中的`paper-world.yml`。具体请见左侧的配置文件指南。  
```yaml
anticheat:
  anti-xray:
    enabled: false
```

### `engine-mode: 2`
主世界：  
请使用以下内容来替代掉 `paper-world-defaults.yml` 中的 `anticheat.anti-xray` 键。  
```yaml
anticheat:
  anti-xray:
    enabled: true
    engine-mode: 2
    hidden-blocks:
    # 你可以添加空气来隐藏洞穴。
    # 这对于反开矿物透视找洞穴的玩家很有用，但是会导致FPS下降。
    - air
    - copper_ore
    - deepslate_copper_ore
    - raw_copper_block
    - diamond_ore
    - deepslate_diamond_ore
    - gold_ore
    - deepslate_gold_ore
    - iron_ore
    - deepslate_iron_ore
    - raw_iron_block
    - lapis_ore
    - deepslate_lapis_ore
    - redstone_ore
    - deepslate_redstone_ore
    lava-obscures: false
    # 1.18版本起，部分矿石的最大生成高度进行了调整。
    # 请自行修改 the max-block-height 以确保适用于当前版本。
    # https://minecraft.fandom.com/wiki/Ore 可能很有帮助
    max-block-height: 64
    replacement-blocks:
    # 箱子无法在模式2中隐藏。
    # 但是如果 max-block-height 调整的足够高，通过藏宝图寻找的箱子也会隐藏。
    - chest
    - amethyst_block
    - andesite
    - budding_amethyst
    - calcite
    - coal_ore
    - deepslate_coal_ore
    - deepslate
    - diorite
    - dirt
    - emerald_ore
    - deepslate_emerald_ore
    - granite
    - gravel
    - oak_planks
    - smooth_basalt
    - stone
    - tuff
    update-radius: 2
    use-permission: false
```

下界：  
复制到地狱文件夹中的`paper-world.yml`。具体请见左侧的配置文件指南。    
```yaml
anticheat:
  anti-xray:
    hidden-blocks:
    # 在上文查看可能绕过的情况与客户端FPS下降的问题。
    - air
    - ancient_debris
    - bone_block
    - glowstone
    - magma_block
    - nether_bricks
    - nether_gold_ore
    - nether_quartz_ore
    - polished_blackstone_bricks
    max-block-height: 128
    replacement-blocks:
    - basalt
    - blackstone
    - gravel
    - netherrack
    - soul_sand
    - soul_soil
```
末地：  
复制到末地文件夹中的`paper-world.yml`。具体请见左侧的配置文件指南。    
```yaml
anticheat:
  anti-xray:
    enabled: false
```
