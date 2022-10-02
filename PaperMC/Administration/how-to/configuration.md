# 配置文件

## 自定义每个世界
强大但不为人所知的Paper功能便是可以为每个世界进行自定义的配置修改。如果你想对每个世界进行默认的设置，则可以尝试使用 `paper-world-defaults.yml` 文件。  

### 默认值
Paper默认不会为每一个世界提供自定义选项，并且将所有默认值存储在 `config/paper-world-defaults.yml` 中。此文件的每一个值都可以被指定世界的指定配置所修改和覆盖，但是默认不会。在此文件中的更改将应用于所有没有修改过指定配置的所有世界。  

### 每个世界的值
要为专门某个世界设定一个配置的值，请在所在世界目录中找到 `paper-world.yml` 。    
例如：你想要为一个叫做 `resource` 的世界禁用 `spawn.keep-spawn-loaded`，则请在 `resource` 文件夹中编辑 `paper-world.yml` 文件。  
就像是这样：  
*此文件位于 resource/paper-world.yml*  
```
_version:  28

spawn:  
  keep-spawn-loaded: false
```
在配置文件中，默认只有 `_version` 的值。要通过添加一个值来默认配置，需要从 `paper-world-defaults.yml` 中复制对应值过来，然后修改。  

### 继承
所有没有明确定义的世界的选项都将保持 `paper-world-defaults.yml` 中的默认配置。  
也就是说，如果想要修改所有世界的默认配置无需机械化的复制、粘贴到每个文件夹里。  
也无需将想要修改的值从 `paper-world-defaults.yml` 挨个复制过来然后粘贴到所有 `paper-world.yml` 文件中。    
只需要复制你想要为某个世界专门定制的选项到对应的 `paper-world.yml` 文件中，然后进行精确的修改即可。    
这有个更加复杂的例子：在两个世界中分别修改 `spawn-limits` 值和 `keep-spawn-loaded` 值。  
  
*位于paper-world-defaults.yml*   
```
entities:  
  spawning:  
    spawn-limits:  
      ambient:  70  
      axolotls:  10  
      creature:  15  
      monster:  5  
      underground_water_creature:  5  
      water_ambient:  5  
      water_creature:  20  
spawn:  
  keep-spawn-loaded:  true
```
*位于world_nether/paper-world.yml*
```
entities:  
  spawning:  
    spawn-limits:  
      monster:  90
```  
*位于resource_world/paper-world.yml*
```
entities:  
  spawning:  
    spawn-limits:  
      axolotls:  8  
      creature:  15  
      monster:  2  
spawn:  
  keep-spawn-loaded:  false
```
这个例子简单的介绍了一下继承的概念。对于目前我们更改的每一个世界，以下列表是正在应用的实际配置：  
![表格](https://i.postimg.cc/rwgvkxFr/QQ-20221001165907.png)  
(如果图片很小，请右键选择在新窗口打开图片。)  
  
值得注意的是，`world_the_end`的值没有被更改过。所以，它继承了 `config/paper-world-defaults.yml` 中的所所有值。
而且，`resource_world/paper-world.yml` 只禁用了 `keep-spawn-loaded`，因为在 `config/paper-world-defaults.yml` 中，该项是启用的。  
