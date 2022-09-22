# 指南
## 下载
### 获取插件
你可以从以下几个方式获取到插件：  
- [Github Releases](https://github.com/kyngs/LibrePremium/releases)  
- [SpigotMC页面](https://www.spigotmc.org/resources/librepremium-bungee-velocity.101040/)  
### 安装
先关闭代理端。    
然后将插件放入/plugins文件夹中，启动代理端。
  
接下来，控制台会打印以下内容：  
```  
[16:39:51 INFO] [librepremium]: Loading configuration...
[16:39:51 WARN] [librepremium]: !! A new configuration was generated, please fill it out, if in doubt, see the wiki !!
```  
然后，可以在生成的LibrePremium插件文件夹中编辑生成的配置文件了。
  
### Limbo 
接下来，你应该选择并配置你的Limbo服务器。绝大多数的人选择使用一个Minecraft服务器作为Limbo。这既不安全，过度奢华，甚至不能容纳过多的玩家。    
作者推荐选择一个专业的Limbo软件，例如[NanoLimbo](https://www.spigotmc.org/resources/nanolimbo-1-8-1-18.86198/)，它即轻量，可配置，也可以容纳很多玩家。  

### 迁移


## 数据库迁移
### 可迁移的插件
*如果你正在使用的身份验证插件还没有被LibrePremium支持，  
请先切换回原有的插件（本地服务器也可）并新建一个随机用户，将密码设定为“testpassword”，然后将该MySQL数据库行导出，在Discord PM作者寻求支持。  *
- JPremium SHA256
- AuthMe BCrypt
- AuthMe SHA256
- Aegis BCrypt
- DynamicBungeeAuth SHA512
- JPremium BCrypt

### 开始迁移
接下来是一个快速的指南，教学如何迁移数据库。  
在配置文件夹中找到`config.conf`，并找到以下内容：  
```
migration {
    old-database {
        # 你的旧数据库名
        database=""
        # 你的旧数据库IP，默认为本机
        host=localhost
        # 你的旧数据库密码
        password=""
        # 你的旧数据库端口
        port=3306
        # 你的旧数据库表
        table=user-data
        # 你的旧数据库用户名
        user=root
    }
    # 是否要在下次启动服务器时，完成迁移工作？
    on-next-startup=false
    # 支持迁移的插件
    # JPremium - Can convert from JPremium SHA256
    # AuthMe - Can convert from AuthMe BCrypt and SHA256
    # Aegis - Can convert from Aegis BCrypt
    # DBA-SHA-512 - Can convert from DynamicBungeeAuth, which was configured to use SHA-512
    type=""
}
```
完成以上配置过程，请重新启动你的代理端。  
LibrePremium将自动完成数据迁移，当完成后，请记得设置`on-next-startup`为false。  
现在你的数据应该迁移完毕，如果出现了什么差错，请记得在GitHub Issue报告。  

## 创建UUID
LibrePremium提供三种自动创建UUID的方式，每一个都有其优缺点。   
**只会对新用户生效**  

### RANDOM（随机）
这个方式非常简单，随机生成UUID。  
请注意：如果你不迁移数据库，玩家的数据将丢失。  

### CRACKED（破解）
与离线模式服务器的工作原理一致。

#### 缺点
让我们想象一下一名叫做`pepazdepavole`的玩家首次加入服务器的情况。  
他的UUID将是`f586c1d8-2314-3df5-bfc4-9ff22f132273`，接下来，玩家启用了自动登录并修改了他们的ID为`kyngs`。不过，即使修改了ID，UUID也不会变化。  
  
现在，又有一名新玩家叫做`pepazdepavole`恰好想要游玩服务器。从逻辑上讲，在数据库中找不到叫做`pepazdepavole`的玩家，应该新建一个新的游戏档案。  
但是，由于他的UUID为`f586c1d8-2314-3df5-bfc4-9ff22f132273`，所以，他会被踢出服务器并要求更改ID为`kyngs`登录。  

**太长不看：**  
玩家如果修改了他们的ID，旧的ID也不能用。  

## Mojang
首先与数据库对比是否存在该用户，如果是，则用正版UUID。否则使用破解UUID。  
缺点和`CRACKED`一样。  





