# 特色功能
## 名称验证
Librepremium将确保每名玩家都有其可用的ID。  
它会强制不区分英文大小写。  
    
目前，它必须：  
- 不超过17个字符。  
- 匹配正则表达式 `[a-zA-Z0-9_]*` （英文小写，英文大写，0-9或者下划线）  
- 与数据库中已有的玩家名称不冲突。  
  
## 自动登录  
LibrePremium允许正版玩家自动登录。  

### 如何启用
输入 `/premium <密码>` 命令来启用它。  
输入 `/cracked` 命令来禁用它。  
  
**注意：玩家一旦启用自动登录，此过程不可逆，并且玩家将无法再次通过破解客户端加入到服务器。**    
**如果有玩家意外地打开了它，管理员必须手动关闭。**  
  
## 自动名称迁移  
*玩家之间的数据迁移从未如此简单过。*     
  
**自动迁移**  
LibrePremium会检测正版玩家（仅启用自动登录的情况下）更改名称，并自动完成玩家的数据迁移（物品栏与插件的数据）。  
  
**手动迁移**  
你可以通过输入 `/librepremium user <旧ID> name <新ID>` 命令进行不同玩家之间的数据迁移工作。  
如果玩家启用了自动登录，也将禁用自动登录。  
  
## 2FA  
LibrePremium是目前市面上唯一一个通过TOTP（Authy，Google Authenticator等软件）支持2FA的代理端身份验证插件。  
想要使玩家的账户更加安全吗？启用2FA功能是个不错的选择。  
  
### 设置2FA
- BungeeCord和Velocity需要安装[Protocolize](https://www.spigotmc.org/resources/protocolize-protocollib-for-bungeecord-waterfall-velocity.63778/)  
- 在配置文件中启用 TOTP，然后填写你的服务器名称  
- 玩家需要访问Limbo服务器（下文），用于扫描2FA二维码。

### 如何使用？
如常访问服务器，并输入 `/2fa` 命令。接下来，玩家将被传送到Limbo服务器。  
玩家需要使用上述TOTP软件扫描Limbo中显示的二维码，然后重新加入服务器。  
一切完成后，登录时便需要2FA了：`/login <密码> <2FA验证码>`  
  
## Floodgate
LibrePremium支持玩家通过基岩版（需要安装Floodgate）加入到服务器中。  

### 安装  
你只需要在代理端安装Floodgate，LibrePremium将自动检测并完成兼容。  

### 它如何工作？
通过基岩版访问服务器，就如同正版玩家加入服务器一样。两者不同的是，基岩版用户将不能使用大多数功能。  
