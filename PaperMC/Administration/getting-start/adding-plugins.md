# 添加插件
插件是从Paper内置的配置文件延申到服务器游戏内容中最强大的办法。插件提供的新功能从可以让牛奶恢复饥饿值、让枯木生长为参天大树，到添加一个原创的游戏玩法。  
>**恶意代码**
>确保你下载的渠道与插件是安全的！插件不但可以无条件的修改服务器，甚至还可以修改你的服务器。因此，请一定确保你下载的插件是安全的。请当心！

## 寻找插件
在安装插件之前，你应该先准备好你想要安装的插件。你可以在 SpigotMC, BukkitDev, 或者在 PaperMC 论坛中找到大多数插件，也有一部分插件在GitHub上发布。  
查找插件的有效途径不是使用内置的搜索功能，而是通过浏览器搜寻。在浏览器中输入`Minecraft plugins`后面跟上你想要搜索插件功能的主要功能，通常可以找到理想的插件。  
> 译者注：
> 别用百度，用必应。必应搜索`Minecraft plugin <加上你要找的插件英文关键字>`

>**Paper与Spigot和Bukkit的兼容性**
>Paper与Bukkit和Paper的插件进行兼容。如果插件没有特别说明不支持Paper服务端，则代表该插件可以在Paper服务器上使用。

## 安装插件
1. 当你寻找到你心仪的插件时，下载它。确保下载的插件以`.jar`结尾。一些插件以`.zip`后缀结尾，则你需要解压缩此压缩文件，得到一份以`.jar`后缀结尾的插件：通常它们会标记为适用于哪个服务端。
2. 当你在本地拥有了你的插件时，找到你的Paper服务器根目录中的`plugins`文件夹。
3. 将`.jar`文件拖拽到plugins文件夹中。如果你使用需要远程连接的服务器，可能需要使用面板或者SFTP上传插件。不过，最终得到的插件和效果是一样的。
4. 重启服务器。插件应该加载了。
5. 检查插件是否生效。当服务器完成加载时，在游戏内输入`/plugins`或者在终端输入`plugins`。对于成功加载的插件，应该在插件列表中是绿色名称。如果没有列出、或者插件为红色则代表没有正常加载，则需要进行故障排查。

## 故障排查
要进行故障排查，第一步是检查你的日志。服务器最新日志会被存储在服务器根目录下的`logs/latest.log`文件里。你需要从头开始阅读整个日志来查看插件在什么时候准备加载。

### 缺少依赖
如果你看到了这样一段文字：
```
Could not load 'plugins/MyAwesomePlugin-1.0.0.jar' in folder 'plugins'  
org.bukkit.plugin.UnknownDependencyException:  Unknown/missing dependency plugins:  [Vault]. Please download and install these plugins to run 'MyAwesomePlugin'.
```
这意味着你尝试安装的插件缺少依赖。通常情况下，依赖是另一个插件，必须在服务器中先安装它后，才会正常加载你想要使用的插件。即使你可能会得到一个长的离谱的报错，但是最重要的一行文本是：  
````
Unknown/missing dependency plugins: [Vault]. Please download and install these plugins to run 'MyAwesomePlugin'.
````
它告诉你：要想正常使用你想要加载的`MyAwesomePlugin`，则必须先安装`Vault`插件。

### 未知的 plugin.yml
如果你看到了类似于以下内容的文本时：
```
Could not load 'plugins/MyAwesomePlugin-1.0.0.jar' in folder 'plugins'
org.bukkit.plugin.InvalidDescriptionException: Invalid plugin.yml
```
这意味着你下载的插件不是一个有效的Paper插件。通常有以下几点原因：  
1. 这根本就不是一个Paper服务端的插件。它是一个适用于Forge、Fabric等等的Mod，因此Paper无法加载它。  
2. 插件未能完全下载。当你使用`curl`或者`wget`等工具时，你可能下载的是网站的某一个页面，而你不是想要下载的插件。也有可能是网络原因，请尝试再次下载插件。如果你通过面板或者SFTP上传的，确保你的SFTP客户端是二进制传输模式，而不是ASCII。查看你使用的SFTP软件文档来了解更多信息。  

### 未知的插件名称
如果你看到类似于以下内容的文本时：  
```
Ambiguous plugin name `Essentials' for files `plugins/EssentialsX-2.19.4.jar' and `plugins/Essentialsx-2.20.0-dev.jar' in `plugins'
```  
这意味着你有两个安装的插件是同名的，Paper不支持这样做。这样就会同时安装了两个`EssentialsX`插件。一个是正式版2.19.4，一个是开发版本2.20.0。确保只安装一个版本的插件，删除旧版本或者你不需要的版本，然后重启服务器。  

### 其它
如果你看到了一个报错，但是和上面却不同，请先尝试自己理解并排查报错。虽然说报错会很长，但是大多数情况下只需要阅读前两行就能明白发生了什么错误。如果还是不确定，请在Discord服务器中找到 #paper-help 频道寻求帮助。  

## 无日志记录
如果你没有找到关于插件的日志，那么你的服务器很有可能根本没有找到这个插件。服务器加载插件需要满足以下条件：  
1. 位于服务器根目录中的`plugins`文件夹中。子目录插件不会被找到，也不会加载，所有插件必须位于`plugins`根目录中。
2. 文件以`.jar`后缀结尾。如果它不以`.jar`结尾，那么你下载的可能根本不是插件。有些作者使用`.zip`文件分发多个插件文件，所以在安装之前，请先解压缩它们。

如果同时满足以上两个条件，但是还是看不到任何关于插件加载的日志，请在Discord服务器中找到 #paper-help 频道寻求帮助。  
