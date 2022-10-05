# Paper Plugin YML

plugin.yml文件是你的插件最主要的配置文件。
包含你的插件最基本的信息，比如插件名，版本和简要描述。同时，也将包含加载插件的依赖，权限和命令。

书接上回。plugin.yml文件存放在你的工程中的 `resources` 文件夹中。就如下图的结构。
```
example-plugin
├── build.gradle.kts
├── settings.gradle.kts
└── src
    └── main
        ├── java
        └── resources
            └── plugin.yml
```

## 例子

这是一个 plugin.yml 的例子：

```yaml
name: ExamplePlugin
version: 1.0.0
main: io.papermc.testplugin.ExamplePlugin
description: An example plugin
author: PaperMC
website: https://papermc.io
api-version: 1.19
```

## 键

> 这部分所有内容的键都无需特定顺序。  
> 如果在它们的旁边有星号，将意味着是必填项目。


### name*

你的插件名。将会在插件列表中（`/plugins`）和日志文本中显示。  
如果设定了前缀，则会被所设定的前缀覆盖。
- `name: ExamplePlugin`

### version*

插件当前的版本。将会在插件信息文本和服务器日志文本中显示。
- `version: 1.0.0`

### main*

插件的主类。是唯一一个继承 `JavaPlugin` 的类，并且是插件的切入点。
- `main: io.papermc.testplugin.ExamplePlugin`

需要包含 包的路径和主类的名字（不用带.java或者.kt）

### description

简短的描述插件是干什么的。将会在插件信息命令中显示。
- `description: An example plugin`

### author / authors

插件的作者（开发者）。可以是单作者或作者列表。  
- `author: PaperMC`
- `authors: [PaperMC, SpigotMC, Bukkit]`
将会在插件信息命令中显示。  

### website

插件的网站。连接到GitHub存储库或是插件发布页很有用。
- `website: https://papermc.io`
将会在插件信息命令中显示。  

### api-version

插件正在使用的 Paper API。不包含次要版本（比如我正在用1.13.2的API，只需要写1.13，不用带 `.2`）  
服务器版本低于此处填写的API版本将直接拒绝加载插件  
有效的版本是1.13-1.19  
- `api-version: 1.19`
  
> 如果没有指定此项，插件将会以legacy plugin加载并且在终端打印警告文本。  

### load

服务器应当在何时加载插件。应该填写 `STARTUP` 或 `POSTWORLD`。
- `load: STARTUP`

### prefix

插件的前缀。在日志中该前缀将取代插件名。
- `prefix: EpicPaperMCHypePlugin`

### libraries

> **警告**    
> 这个功能目前违反maven central的ToS。不过嘛，这个功能很有可能保留下来。

> **译者说明**    
> 下面的第二行我不确定啥意思，原文在下面列出来了。

列出你的插件需要依赖的libraries。这些libraries将会从Maven central存储库下载并加到 classpath 中。  
无需shade和relocate libraries。
- 原文：`This removes the need to shade and relocate the libraries.`
```yaml
libraries:
  - com.google.guava:guava:30.1.1-jre
  - com.google.code.gson:gson:2.8.6
```

### permissions

列出你的插件所需的权限。对应限制哪些玩家应该可以使用哪些功能很有用。  
```yaml
permissions :
  - permission.node:
        description: "This is a permission node"
        default: op
        children:
            - permission.node.child: true
  - another.permission.node:
        description: "This is another permission node"
        default: not op
```

description是权限节点的描述。将会在权限列表中显示。default是权限节点的默认值，可以设为为 `op`/`not op`或`true`/`false`。此值默认是 `op`。    
每个权限节点都可以有子权限。当设定为 `true` 时它将继承父权限。  

## Commands

列出插件使用的命令。如果需要使用命令访问某些功能时很有用。
```yaml
commands:
  - command:
        description: "This is a command"
        usage: "/command <arg>"
        aliases: [cmd, command]
        permission: permission.node
        permission-message: "You do not have permission to use this command"
```

-  **description**是命令的描述。简要的描述命令的作用。
-  **usage**是命令的用法。将会在玩家运行 `/help <command>` 命令时显示。
-  **aliases** 是命令使用的一系列别名。对于缩短命令很有帮助。
-  **permission**是玩家要使用此命令所需的权限节点。注意：玩家只有当他们有权限使用时才会显示命令。
-  **permission-message**在玩家没有权限使用命令时显示的内容。

## Dependencies:

> **依赖循环:**   
当玩家为插件指定依赖时，它会在你的插件加载之前优先加载。  
如果插件依赖重复则会导致问题。依赖循环具体会产生以下问题：
插件A -> 依赖插件B -> 依赖插件A -> 又依赖插件B... 等等。  
>   
> 因为插件A和插件B都是彼此的依赖。（套娃）

### depend

列出插件**加载**时的依赖。需要指定插件名称。

> 如果指定插件找不到，你的插件也不会加载。

- `depend: [Vault, WorldEdit]`

### softdepend

要使用插件全部功能的依赖列表（软依赖。不用这些插件也能正常加载插件，但是不能访问全部功能）。需要指定插件名称。

- `softdepend: [Vault, WorldEdit]`

### loadbefore

列出插件优先加载的插件列表。需要指定插件名称。  
若需要优先加载你的插件，在某些插件需要使用你的插件的API时很有用。

- `loadbefore: [Vault, FactionsUUID]`
