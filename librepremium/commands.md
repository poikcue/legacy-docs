# 命令

## 身份验证命令
`/login <密码>` 尝试使你登录（无需权限）  
`/register <密码> <重复密码>` 尝试为你注册（无需权限） 

## 正版相关命令
`/premium <密码>` 启用自动登录（无需权限。此命令相关内容详见上一页。）  
`/cracked` 禁用自动登录（无需权限）  

## 管理员命令
`/librepremium <子命令>` 需要提供子命令（需要对应子命令权限）

### 重载
`/librepremium reload <重载子命令>` 需要提供子命令（需要对应子命令权限）  
  
`/librepremium reload configuration` 重载配置文件（需要librepremium.reload.configuration权限）  
`/librepremium reload messages` 重载语言文件（需要librepremium.reload.messages权限）

### 为玩家
`/librepremium user <subcommand>` 需要提供子命令（需要对应子命令权限）   
   
`/librepremium user info <name>` 显示玩家信息（UUID，正版UUID，加入服务器日期与最后活跃日期）（需要librepremium.user.info权限）  
`/librepremium user migrate <name> <newName>` 迁移玩家数据，详情见上一页（需要librepremium.user.migrate权限）  
`/librepremium user unregister <name>` 取消注册某玩家，但是下一名同ID玩家将会继承此玩家的数据（背包，进度等等）（需要librepremium.user.unregister权限）  
`/librepremium user delete <name>` 删除玩家数据 **这些数据将永远丢失，且无法找回。最好用取消注册命令代替。**（需要librepremium.user.delete权限）  
`/librepremium user premium <name>` 启用自动登录（需要librepremium.user.premium权限）  
`/librepremium user cracked <name>` 禁用自动登录并切换为破解模式（需要librepremium.user.cracked权限） 
`/librepremium user register <name> <password>` 指定一个用户名和密码注册（需要librepremium.user.register权限）  
`/librepremium user login <name>` 登录账户（假定此玩家在线，但是未经验证）（需要librepremium.user.login权限）  
`/librepremium user 2faoff <name>` 禁用某玩家的2FA（需要librepremium.user.2faoff权限）  
  
## 其它命令
`/changepassword <旧密码> <新密码>` 更改密码（无需权限）  
`/2fa` 启用2FA，详情见上一页。  
