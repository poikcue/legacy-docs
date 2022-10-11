# Paper 工程设置

> **译者注**  
> 本文的图片都是由译者提供的。供新手开发者找到文章提到的选项。

由于Paper团队主要使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/) 进行开发，所以本指南将以该IDE作为重点。    
不过，下文应当也适用于其它IDE，仅需针对性的作一些微小的修改即可。  

Paper团队使用 [Gradle](https://gradle.org/) 作为构建工具，同时也需要Gradle进行构建。    
在经过修改后，下文的代码在修改后也将适用于其它构建工具，比如Maven，但是本文中的代码将只适用Gradle。

遵循 [此](https://docs.gradle.org/current/userguide/migrating_from_maven.html) 文档学习如何从Maven迁移到Gradle。

### 创建新工程

打开你的IDE然后点击创建新工程的按钮。  
[![xlD8wq.png](https://s1.ax1x.com/2022/10/05/xlD8wq.png)](https://imgse.com/i/xlD8wq)  
在Intellij中，你需要选择你想要创建的工程类型 - 选择 `New Project`，然后选择 `Gradle - Kotlin DSL` 后单击 `Create`。    

[![xlDYkV.png](https://s1.ax1x.com/2022/10/05/xlDYkV.png)](https://imgse.com/i/xlDYkV)    

接着，你将在IDE中自动重定向到可添加工程依赖的 `build.gradle.kts` 文件。  

### 将Paper作为依赖

要将Paper作为依赖，你需要将Paper存储库和其依赖本身添加到你的 `build.gradle.kts` 文件中。  

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

### 设立 `src` 目录

> **跳过**  
> 如果IDE已经为你的工程自动创建 `src` 目录，你就可以跳过这一步了。

要设立 `src` 目录，你需要新建一个命名为 `src` 的文件夹然后再在里面创建子目录，叫做 `main`。  
然后，在`Main`之中创建两个文件夹，分别命名为 `java` 和 `resources`。  

该文件夹现在应该长得像这样：

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

### 设立 `java` 目录

你需要在`java`目录中存放你的Java代码。你必须先创建一些包来管理你的Java代码。
拿下面这个结构举例，我们创建了三个包并将其命名为 `io.papermc.testplugin`。而在包中有一个`ExamplePlugin`。

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

可以看到，`ExamplePlugin`类（class）在 `io.papermc.testplugin` 包中。  
包是管理你的代码的方式。本质上，包就是个文件夹。在Java中，使用包以管理其涉及到的代码。  
如果你想要阅读更多关于包的信息，你可以在Oracle的指南中[查看](https://docs.oracle.com/javase/tutorial/java/package/packages.html)。  

要为你的包[命名](https://docs.oracle.com/javase/tutorial/java/package/namingpkgs.html)，你需要将域名倒序排列。比如你有一个叫做 `papermc.io`的域名，你的包应该命名为 `io.papermc`。  
如果你还没有一个域名，你可以将类似于你的GitHub用户名的东西作为包名。  
若你的名字叫做 Linus Torvalds，你的包应该是 `io.github.torvalds`。  

跟随包名后面的应该是你的工程名。  
比如，如果你的工程叫做 `ExamplePlugin`，你的包应该是`io.github.torvalds.exampleplugin`。  
这将为你每个插件取一个独一无二包名。

### 主类

并且也是你的插件中唯一一个继承 `JavaPlugin` 的类。 
你的 `ExamplePlugin` 类应当看上去像是这样：

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

### 设立 `resources` 

该 `resources` 文件夹是你开发的插件存放 `plugin.yml` 的地方。查看左侧 Plugin Yml页面以了解更多信息。  

### 最后

现在，你应当有一个将Paper作为依赖的工程啦！  
你现在只需要编译你的插件，然后跑在Paper服务器上使用插件就好。  

> **注：**  
> 如果你想要快速测试你的插件，你可以 [Run-Paper](https://github.com/jpenilla/run-paper) Gradle task。  
> 它将自动下载Paper服务器并为服务于你的插件。  

> **详细信息：**    
> 如果你正在使用IntelliJ，你应使用 Gradle GUI `Build` 菜单来编译你的插件 - 在你的IDE的右上角。
> 你的输出的jar应该存放在 `build/libs` 文件夹中。
