# 监听事件

 `Events`（事件）是在游戏中监听具体的某个特定行动的最有效的方式。它们可以被服务器或插件所调用。  
当发生某事时，它们将被服务器或插件所调用，例如某名玩家加入了服务器，或是某玩家破坏了某个方块。  
插件能够调用自定义事件，例如玩家完成了某个任务或被其它插件所监听的事件。  

## 你的监听器类

要监听一项事件，你需要创建一个类并实现 `Listener`。  
你想要为该类取什么名称都行，不过建议命名为你与所监听的事件相关的名称。  

```java
public class ExampleListener implements Listener {
    // ...
}
```

## `@EventHandler`

要监听某事件，你需要创建一个方法（method）并注释为 `@EventHandler`。  
同样，你想要为该方法取什么名称都行。但是建议命名为有助于理解你所监听的事件的名称。  

## 监听器方法

Method Body 无需返回任何数据，因为使用 `void` 就视为返回的类型。
listener接受该事件所监听到的单个参数。
    
```java
public class ExampleListener implements Listener {

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent event) {
        // ...
    }
}
```

> 由于篇幅有限，这里没有列出所有可监听事件的列表。不过在    
> [这里](https://jd.papermc.io/paper/1.19/org/bukkit/event/Event.html) 可以了解所有继承 `Events` 的类。  

## 注册监听器

要注册监听器，你需要调用 `Bukkit.getPluginManager().registerEvents()` 并传入监听器类的实例和你的插件的实例。  
  
 将会注册监听器类并允许它监听所有事件。    
 通常会在你的插件的 `onEnable()` 方法中，所以一般会在服务器开始Ticking注册。

```java
public class ExamplePlugin extends JavaPlugin {

    @Override
    public void onEnable() {
        getServer().getPluginManager().registerEvents(new ExampleListener(), this);
    }
}
```

## 事件优先级

你也可以指定事件的优先级。  
    
```
public class ExampleListener implements Listener {

    @EventHandler(priority = EventPriority.HIGH)
    public void onPlayerJoin(PlayerJoinEvent event) {
        // ...
    }
}
```
你可以选择六个不同的优先级：
- `EventPriority.LOWEST`
- `EventPriority.LOW`
- `EventPriority.NORMAL`
- `EventPriority.HIGH`
- `EventPriority.HIGHEST`
- `EventPriority.MONITOR`

实际上优先级的顺序与直觉相反。优先级 **越高**，事件被调用就 **越晚**。  
例如：你的插件中有某些事件超级重要（需要放到最后调用）- 以避免被更改 - 则需要使用`EventPriority.HIGHEST`  

> **注意**  
> `MONITOR` 的优先级常常用于监视事件，而不会更改它。它在所有优先级中最后才会调用。  
> 这就意味着可得到不同插件之间相互影响的结果，例如取消（cancellation）和修改（modification）。  

## 取消事件

一些事件可以取消，阻止某些行动的完成。这些事件实现 `Cancellable`。  
    
```java
public class ExampleListener implements Listener {

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent event) {
        event.setCancelled(true);
    }
}
```

> 在你的插件调用之前请思考一下其它插件是否会取消或更改该事件。    
> 在做某些事之前先检查这些事件吧！    

上面的例子会取消事件，就意味着玩家无法加入到服务器中。当一个事件被取消，它将会其它事件继续调用监听器，除非在 `@EventHandler` 注释中添加了 `ignoreCancelled = true` 以忽略已取消的事件。  
像是这样：
```
public class ExampleListener implements Listener {

    @EventHandler(ignoreCancelled = true)
    public void onPlayerJoin(PlayerJoinEvent event) {
        // ...
    }
}
```
