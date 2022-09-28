# 有用的玩意
## 配置文件
**此配置文件部分内容可能与实际内容不一致**  
*中文版配置文件仅供参考，以英文页面内容为准。*  
*请同时对照英文Wiki与本地生成的配置文件按照需求修改。*  
*由于我不是插件作者，中文版配置文件可能不会及时更新，请谅解*  
```
#  !!此配置文件使用HOCON语法!!
#  hocon语法与Json类似，但是它额外添加了一些功能
#  你可以在此页面中找到关于hocon的更多信息
#  https://docs.spongepowered.org/stable/en/server/getting-started/configuration/hocon.html
#  ----------------------------------------------------------------------------------------
#  LibrePremium 配置文件
#  ----------------------------------------------------------------------------------------
#  这是 LibrePremium 的配置文件。
#  你可以在GitHub上找到关于 LibrePremium的更多信息。
#  https://github.com/kyngs/LibrePremium

# 玩家在验证身份（注册或登录之前）时只能用哪些命令？
allowed-commands-while-unauthorized=[
    login,
    register
]
# 是否应该为正版玩家自动注册？
# !!破解玩家将无法用正版用户名注册!!
auto-register=false
database {
    # 数据库缓存时间（单位：秒）
    cache=600
    # 数据库名
    database=librepremium
    # 数据库主机IP（默认为本机）
    host=localhost
    # 数据库密码
    password=""
    # 数据库端口
    port=3306
    # 数据库用户名
    user=root
}
# 加密方式，安全起见，将用于加密玩家的密码。支持以下加密方式：
# SHA-256 - 旧的加密方式，不推荐。出于兼容目的保留。
# SHA-512 - 比SHA-256安全点，但是还是不推荐。出于兼容目的保留。
# BCrypt-2A - 更新，更安全。
default-crypto-provider=BCrypt-2A
# 如果玩家输入了错误的密码，是否要踢出服务器？
kick-on-wrong-password=false
# 玩家在验证身份时的服务器，这个服务器必须在代理端的配置文件中注册为一个子端。
limbo=""
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
    # JPremium - 可以从 JPremium SHA256 转换
    # AuthMe - 可以从 AuthMe BCrypt 与 SHA256 转换
    # Aegis - 可以从 Aegis BCrypt 转换
    # DBA-SHA-512 - 可以从 DynamicBungeeAuth 转换，需要为 SHA-512 加密。
    type=""
}
# 多久通知一次玩家进行身份验证？设置为负数可以禁用此功能。
# 包括但不限于：
# - 聊天栏发送的文本
# - 标题（Title）
milliseconds-to-refresh-notification=10000
# UUID创建方式。
# 详见 https://docs.poikcue.com/#/librepremium/guide#%E5%88%9B%E5%BB%BAuuid
new-uuid-creator=RANDOM
# 完成身份验证后玩家应该传送到哪个服务器？这些服务器必须在代理端的配置文件中注册为子端。
pass-through=[
    lobby0,
    lobby1
]
# 配置文件版本 !!不要修改此项!!
revision=0
# 玩家多长时间未完成身份验证后踢出服务器？
seconds-to-authorize=-1
# 身份验证通知是否需要在标题（Title）中显示？
use-titles=true
```

## 语言文件
**此消息文件部分内容可能与实际内容不一致**  
*中文版消息文件仅供参考，以英文页面内容为准。*  
*请同时对照英文Wiki与本地生成的消息文件按照需求修改。*  
*由于我不是插件作者，中文版消息文件可能不会及时更新，请谅解*  
```
#  !!此配置文件使用HOCON语法!!
#  hocon语法与Json类似，但是它额外添加了一些功能
#  你可以在此页面中找到关于hocon的更多信息
#  https://docs.spongepowered.org/stable/en/server/getting-started/configuration/hocon.html
#  ----------------------------------------------------------------------------------------
#  LibrePremium 消息
#  ----------------------------------------------------------------------------------------
#  此插件提供的所有（可修改）消息。你可以根据个人或服务器需求更改它们。
#  你可以在GitHub上找到关于 LibrePremium的更多信息。
#  https://github.com/kyngs/LibrePremium

# 已完成身份验证后再次尝试使用身份验证命令的提示内容。
error-already-authorized="你已经授权了！"
# 已注册玩家再次尝试使用注册命令的提示内容。
error-already-registered="你已经注册了。"
# 读取配置文件失败（或出现问题）时提示的内容。
error-corrupted-configuration="配置文件损坏，或读取出现问题，将使用旧配置文件。原因：%cause%"
# 读取消息文件（messages.conf）失败（或出现问题）时提示的内容。
error-corrupted-messages="消息文件损坏，或读取出现问题，将使用旧消息文件。原因：%cause%"
# 当玩家使用错误的命令用法时提示的内容。
error-invalid-syntax="Usage: <c2>{command}</c2> <c3>{syntax}</c3>"
# 当玩家在输入/premiumconfirm之前未输入过/premium时提示的内容。
error-no-confirm="请先使用 /premium <密码> 验证！"
# 当玩家尝试使用某命令时权限不足时提示的内容。
error-no-permission="你没有使用此命令的权限！"
# 当玩家在未完成授权时尝试使用需要授权的命令时提示的内容。
error-not-authorized="请先验证身份！"
# 当已启用自动登录的玩家再次输入启用自动登录的命令时提示的内容。
error-not-cracked="你已启用自动登录。使用 /cracked 来禁用自动登录！"
# 当玩家尝试启用自动登录时，在Mojang数据库中找不到对应的用户时提示的内容。
error-not-paid="我们在Mojang数据库中找不到你的账户。"
# 当未启用自动登录的玩家尝试禁用自动登录时提示的内容。
error-not-premium="你还没有启用自动登录。禁用自动登录前，使用 /premium <密码> 启用自动登录！"
# 当未注册玩家尝试使用登录命令时提示的内容。
error-not-registered="请先注册！"
# 当玩家准备迁移数据到一个已使用的用户名时提示的内容。
error-occupied-user="此用户名已被占用！"
# 当玩家使用一个不可用的密码时提示的内容。
error-password-corrupted="此密码不可用，要解决此问题，请与服务器管理员联系。"
# 当玩家使用不同的密码进行注册时提示的内容。
error-password-not-match="密码不匹配，请重试。"
# 当玩家尝试使用错误的密码进行授权时提示的内容。
error-password-wrong="错误的密码。"
# 当玩家尝试与已授权玩家进行相关的操作时提示的内容。
error-player-authorized="此玩家已授权！"
# 当玩家尝试与未注册玩家进行相关的操作时提示的内容。
error-player-not-registered="此玩家未注册！"
# 当玩家尝试与离线玩家进行相关的操作时提示的内容。
error-player-offline="此玩家目前处于离线状态！"
# 当玩家尝试与在线玩家进行相关的操作时提示的内容。
error-player-online="此玩家目前处于离线状态！"
# 当服务器触及Mojang API限制（600次请求/10分钟）时对玩家提示的内容
error-premium-throttled="服务器已经触发Mojang API限制，请稍后再试"
# 当与Mojang API连接时出现问题，我们无法验证玩家是否为正版。
# 如果出现了此问题，则控制台也会同时打印相关内容。
error-premium-unknown="与Mojang API通信时出现了点问题。请向服务器管理员寻求帮助，或查看控制台错误信息。"
# 当玩家发送命令过快时提示的内容。
error-throttle="等一下！你发送命令的速度太快了，请稍后再试。"
# 当出现未知的错误时提示的内容。
error-unknown="出现了一个未知的问题。请向服务器管理员寻求帮助，或查看控制台错误信息。"
# 当玩家使用未知的命令时提示的内容。
error-unknown-command="未知的命令。"
# 当玩家尝试与无效的玩家进行相关的操作时提示的内容。
error-unknown-user="此用户不存在！"
# 删除了某些东西时提示的内容。
info-deleted="已删除！"
# 正在删除某些东西时提示的内容。
info-deleting="删除中..."
# 正在某些东西时提示的内容。
info-disabling="禁用中..."
# 修改了某些东西时提示的内容。
info-edited="已修改！"
# 正在修改某些东西时提示的内容。
info-editing="修改中..."
# 正在启用某些东西时提示的内容。
info-enabling="启用..."
# 玩家成功登录时提示的内容。
info-logged-in="已登录！"
# 当玩家尝试进行登录时提示的内容。
info-logging-in="登录中..."
# 玩家成功注册时提示的内容。
info-registered="已注册！"
# 当玩家尝试进行注册时提示的内容。
info-registering="注册中..."
# 重载了某些东西时提示的内容。
info-reloaded="已重载！"
# 正在重载某些东西时提示的内容。
info-reloading="重载中..."
# 当请求查看玩家信息时提示的内容。
info-user="UUID: %uuid%\n正版 UUID: %premium_uuid%\n最后活跃: %last_seen%\n加入时间: %joined%\n"
# 当玩家名称验证时不通过踢出时提示的内容。
# 详见 https://docs.poikcue.com/#/librepremium/feature#%E5%90%8D%E7%A7%B0%E9%AA%8C%E8%AF%81
kick-illegal-username="名称中含有非法字符或超过最大16个字符限制。"
# 当玩家大小写不匹配时提示的内容。
# 详见 https://docs.poikcue.com/#/librepremium/feature#%E5%90%8D%E7%A7%B0%E9%AA%8C%E8%AF%81
kick-invalid-case-username="请切换到用户名至 &c%username%"
# 当存档冲突时提示的内容。
# 详见 https://docs.poikcue.com/#/librepremium/considerations#%E5%AD%98%E6%A1%A3%E5%86%B2%E7%AA%81
kick-name-mismatch="哦，不！有一个正版玩家将用户名修改为了 %nickname%，导致有两个冲突的用户名。请与管理员联系解决此问题！"
# 当全部服务器已满或不可用时提示的内容
kick-no-server="没有服务器可用，请稍后再试。"
# 当玩家的用户名已占用时提示的内容。
kick-occupied-username="请切换用户名至 &c%username%"
# 当服务器触及Mojang API限制（600次请求/10分钟）时对玩家提示的内容
kick-premium-error-throttled="服务器已经触发Mojang API限制，请稍后再试"
# 当与Mojang API连接时出现问题，我们无法验证玩家是否为正版。
# 如果出现了此问题，则控制台也会同时打印相关内容。
kick-premium-error-undefined="与Mojang API通信时出现了点问题。请向服务器管理员寻求帮助，或查看控制台错误信息。"
# 当玩家禁用自动登录后踢出服务器的提示内容.。
kick-premium-info-disabled="自动登录已禁用！"
# 当玩家启用自动登录后踢出服务器的提示内容.。
kick-premium-info-enabled="自动登录已启用！"
# 服务器等待玩家进行授权的时间过长，踢出玩家时提示的内容（可以在配置文件中修改。）
kick-time-limit="你花了太长时间进行身份验证，请重试！"
# 提醒玩家确认启用自动登录时提示的内容。
prompt-confirm="即将为你的账户启用自动登录。请注意：一旦启用了自动登录，你将&4无法&r从破解客户端登录到服务器。稍后，你可以手动 /cracked 禁用自动登录。如果你确认要启用自动登录，请在聊天栏输入 /confirmpremium 命令。"
# 当玩家尝试登录时聊天栏提示的内容。
prompt-login="请登录: /login <密码>"
# 当玩家尝试注册时聊天栏提示的内容。
prompt-register="请使用此命令注册: /register <密码> <重复密码>"
# 配置文件版本号 !!不要动此项!!
revision=0
# 玩家尝试登录时显示的副标题，要显示此内容，请在配置文件中修改 use-titles 项为 true。
sub-title-login="&b请查看聊天栏进行登录"
# 玩家尝试注册时显示的副标题，要显示此内容，请在配置文件中修改 use-titles 项为 true。
sub-title-register="&b请查看聊天栏进行注册"
# 玩家尝试登录时显示的标题，要显示此内容，请在配置文件中修改 use-titles 项为 true。
title-login="&b登录"
# 玩家尝试注册时显示的标题，要显示此内容，请在配置文件中修改 use-titles 项为 true。
title-register="&b注册"
```
