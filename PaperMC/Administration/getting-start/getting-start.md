
# 让我们开始吧
## 需求
> 注意：  
> 随着1.18版本的发布，Paper现在需要**Java17**才能正常运行。如果你还没有使用Java17，请下载它。  

| Paper版本 | 建议Java版本 |
|--|--|
| 1.8 - 1.11 | Java8 |
| 1.12 - 1.16.4 | Java 11 |
| 1.16.5 | Java 16 |
| 1.17 - 1.18.1 或更高 | Java 17 |

## 迁移存档到Paper
### 从Vanilla（原版）迁移：
从原版迁移到Paper相当容易，但是存档有点不同：Paper（或CraftBukkit或Spigot）将不同的维度单独分成不同的文件夹。  
不用担心！Paper会自动帮助你完成存档转换  

### 从CraftBukkit或Spigot迁移：
Paper是CraftBukkit或Spigot开箱即用的替代品（Fork），所以你无需为此作任何事情。  
  
## 下载Paper
Paper在网站提供了可以直接下载的Jar文件：[官方网站下载地址](https://papermc.io/downloads)。
选择游戏版本和所需下载的构建版本号即可。  

## 启动服务器
启动服务器与启动其它Java程序一样。   
  
打开你的终端，然后切换到存放服务器数据的文件夹（如果你是第一次启动，应该只在空文件中放入上文下载的Paper服务端），然后运行`java -Xms2G -Xmx2G -jar paper.jar --nogui`。  
你需要将`paper.jar`修改成你下载的文件名。
    
你想要调整分配的内存，只需要修改`-Xms`和`-Xmx`参数。并且使用`--nogui`禁用原版服务端的GUI。
如果使用了`--nogui`参数，你将不会得到两个界面（一个终端一个GUI）。  
  
要对此参数进行更细致的调整，详见左侧 Aikar's Flags 一文。  
