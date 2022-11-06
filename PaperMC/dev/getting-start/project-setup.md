# Paper 项目的搭建

> **译者注**  
> 本文的图片都是由译者提供的。供新手开发者找到文章提到的选项。

有鉴于 Paper 团队成员主要使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/) 进行开发，本指南着重介绍使用该 IDE 搭建项目之流程。    
不过，下文步骤亦适用于其它 IDE ，仅需针对性地作一些微小的修改即可。  

Paper 团队以 [Gradle](https://gradle.org/) 为自身 PaperMC 等项目之构建工具，其插件开发工具链亦系为用 Gradle 进行依赖管理之项目所设计。故此文仅涉及 Gradle 项目之搭建。下文代码经修改后亦可供其他如 Maven 等构建工具使用。

阅读[此文档](https://docs.gradle.org/current/userguide/migrating_from_maven.html)学习如何将 Maven 项目迁移至 Gradle。

### 创建新项目

打开你的 IDE 然后点击创建新项目的按钮。  
[![xlD8wq.png](https://s1.ax1x.com/2022/10/05/xlD8wq.png)](https://imgse.com/i/xlD8wq)  
在 Intellij 中，你需要选择你想要创建的项目类型 —— 首先选中 `New Project`，然后选中 `Gradle - Kotlin DSL` 再单击 `Create`。    

[![xlDYkV.png](https://s1.ax1x.com/2022/10/05/xlDYkV.png)](https://imgse.com/i/xlDYkV)    

接着，IDE 将自动为你打开可用于管理项目依赖的 `build.gradle.kts` 文件。  

### 将 Paper 作为依赖项添加

要将 Paper 作为插件项目的一个依赖项，你需要将 Paper 仓库 ( `repository` ) 和 Paper 依赖 ( `dependency` ) 添加到你的 `build.gradle.kts` 文件中。  

```kotlin
repositories {
    mavenCentral()
    maven("https://repo.papermc.io/repository/maven-public/")
}

dependencies {
    compileOnly("io.papermc.paper:paper-api:1.19.2-R0.1-SNAPSHOT")
}

java {
    toolchain.languageVersion.set(JavaLanguageVersion.of(17))
}
```

### 创建 `src` 目录

> **注：**  
> 如果 IDE 已经为你的项目自动创建了 `src` 目录，你就可以跳过这一步了。

要创建 `src` 目录，你需要新建一个名为 `src` 的文件夹，然后在其内创建子目录，命名为 `main`。  
然后，在 `main` 中创建两个文件夹，分别命名为 `java` 和 `resources`。  

该文件夹的目录结构形如：

```
...
example-plugin
├── build.gradle.kts
├── settings.gradle.kts
└── src
    └── main
        ├── java
        └── resources
...
```

### 创建 `java` 目录

Java 源代码存放在 `java` 目录中。你必须先创建一些包来管理你的 Java 代码。
拿下面这个结构举例，我们创建了一个三层的包并将其命名为 `io.papermc.testplugin`。而在包中有一个 `ExamplePlugin` 类 ( `class` )。

```
...
example-plugin
├── build.gradle.kts
├── settings.gradle.kts
└── src
    └── main
        ├── java
        │   └── io
        │       └── papermc
        │           └── testplugin
        │               └── ExamplePlugin.java
        └── resources
...
```

### 包

可以看到，`ExamplePlugin` 类在 `io.papermc.testplugin` 包中。  
包用于管理代码。本质上，包就是个文件夹。在 Java 中，我们用包来管理一组相互间有一定关联的类。  
如果你想要了解更多关于包的信息，你可以在 Oracle 的[指南](https://docs.oracle.com/javase/tutorial/java/package/packages.html)中查看。  

要为你的包[命名](https://docs.oracle.com/javase/tutorial/java/package/namingpkgs.html)，你需要将域名倒写。比如有一个叫做 `papermc.io`的域名，你的包就应该命名为 `io.papermc`。  
如果你还没有一个域名，你可以将你的 GitHub 用户名作为包名（格式大概是：`io.github.用户名`）。  
若你的名字叫做 Linus Torvalds，你的包应该是 `io.github.torvalds`。  

跟随域名的应该是你的项目名。  
比如，你有一个项目叫做 `ExamplePlugin`，你的包名应该是`io.github.torvalds.exampleplugin`。  
如此命名后，你的每个插件都会有一个独一无二的包名。

### 主类

主类是你的插件中所有代码执行的起点，是唯一一个继承 `JavaPlugin` 的类。 
如下是一个 `ExamplePlugin` 类的示例：

```java
package io.papermc.testplugin;

import net.kyori.adventure.text.Component;
import org.bukkit.Bukkit;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerJoinEvent;
import org.bukkit.plugin.java.JavaPlugin;

public class ExamplePlugin extends JavaPlugin implements Listener {

    @Override
    public void onEnable() {
        Bukkit.getPluginManager().registerEvents(this, this);
    }

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent event) {
        event.getPlayer().sendMessage(Component.text("Hello, " + event.getPlayer().getName() + "!"));
    }

}
```

### 创建 `resources` 目录

`resources` 文件夹是在你的插件中存放 `plugin.yml` 的地方。在[这里](https://docs.poikcue.com/#/PaperMC/dev/getting-start/plugin-yml)了解更多关于 plugin.yml 的信息。  

### 最后

现在，你就有一个将 Paper 作为依赖的插件项目啦！  
剩下的不过是编译你的插件，然后在 Paper 服务器上运行插件，即可大功告成。  

> **注：**  
> 如果你想要精简测试插件的流程，你可以使用 [Run-Paper](https://github.com/jpenilla/run-paper) Gradle task。  
> 它将帮你自动下载一个 Paper 服务端并运行，以便测试你的插件。  

> **提示：**    
> 如果你正在使用 IntelliJ，你可以使用 Gradle 图形界面中的 `Build` 菜单来编译你的插件 - 它应该位于你的 IDE 的右上角。
> 编译成功后输出的 jar 文件应该存放在 `build/libs` 文件夹中。
