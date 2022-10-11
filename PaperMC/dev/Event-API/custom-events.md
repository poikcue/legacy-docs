# 自定义事件

创建自定义事件是为你的插件添加新功能的不错的方式。    
这将允许其它插件监听你的自定义事件并为你的插件添加新功能。

## 创建一个自定义事件

要创建一个自定义事件，你需要创建一个类并继承 `Event`。每个事件都需要一个 `HandlerList` 以包含所有监听到该事件的监听器。  
不过例外的是，当你有一个无法启动的事件类时，需要用其它事件替代来充当父级。  
  
这有一个不能直接监听 `BlockPistonEvent` 的例子。

该列表用于当事件被调用时，调用监听器。

> **关于`getHandlerList`的信息：**  
> 尽管它不是从 `Event` 继承，不过你仍需要添加一个静态 `getHandlerList()` 方法并为你的事件返回 `HandlerList`。  
> 若要使你的事件正常工作，则需要使用这两个方法。  

```java
public class PaperIsCoolEvent extends Event {

    private static final HandlerList HANDLER_LIST = new HandlerList();

    public static HandlerList getHandlerList() {
        return HANDLER_LIST;
    }

    @Override
    public HandlerList getHandlers() {
        return HANDLER_LIST;
    }
}
```

现在已经创建了我们的事件，我们现在可以为它添加许多功能啦！  
事件被调用时，或许这会向服务器发送一条包含消息的广播。

```java
public class PaperIsCoolEvent extends Event {

    private static final HandlerList HANDLER_LIST = new HandlerList();
    private Component message;

    public PaperIsCoolEvent(Component message) {
        this.message = message;
    }

    public static HandlerList getHandlerList() {
        return HANDLER_LIST;
    }

    @Override
    public HandlerList getHandlers() {
        return HANDLER_LIST;
    }

    public Component getMessage() {
        return this.message;
    }
    
    public void setMessage(Component message) {
        this.message = message;
    }
}
```

## 调用事件

现在，我们已经创建了这个事件。我们可以调用它了。  

```java
public class ExamplePlugin extends JavaPlugin {

    // ...

    public void callCoolPaperEvent() {
        PaperIsCoolEvent coolEvent = new PaperIsCoolEvent(Component.text("Paper is cool!"));
        coolEvent.callEvent();
        // 插件本来就可以够从它们的监听器内部更改消息的。所以我们需要重新获取消息。
        // 此事件结构允许其它插件从它们那里更改消息。
        // 举个例子：一个插件为所有消息添加了前缀！
        Bukkit.broadcast(coolEvent.getMessage());
    }
}
```

## 取消实现

如果你想要允许你的事件被取消，则可以实现 `Cancellable` 接口。

```java
public class PaperIsCoolEvent extends Event implements Cancellable {

    private static final HandlerList HANDLER_LIST = new HandlerList();
    private Component message;
    private boolean cancelled;

    // ...

    @Override
    public boolean isCancelled() {
        return this.cancelled;
    }

    @Override
    public void setCancelled(boolean cancelled) {
        this.cancelled = cancelled;
    }
}
```

现在，当事件被调用时，你就可以检查它是否被取消了。

```java
public class ExamplePlugin extends JavaPlugin {

    // ...

    public void callCoolPaperEvent() {
        PaperIsCoolEvent coolEvent = new PaperIsCoolEvent(Component.text("Paper is cool!"));
        coolEvent.callEvent();
        if (!coolEvent.isCancelled()) {
            Bukkit.broadcast(coolEvent.getMessage());
        }
    }
}
```
当一个事件为cancellable并且事件已经被取消，`Event#callEvent` 则会返回 `false`。这就允许你直接在if语句中使用 `callEvent` 所输出的结果，而无需手动检查 `Cancellable#isCancelled`了。  
  
```java

public class ExamplePlugin extends JavaPlugin {

// ...

public class ExamplePlugin extends JavaPlugin {
    // ...
    public void callCoolPaperEvent() {
        PaperIsCoolEvent coolEvent = new PaperIsCoolEvent(Component.text("Paper is cool!"));
        if (coolEvent.callEvent()) { // 直接从callEvent获取输出结果。
            Bukkit.broadcast(coolEvent.getMessage());
        }
    }
}

```
