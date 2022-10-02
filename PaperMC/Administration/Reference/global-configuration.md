
# Paper 全局配置

全局配置将应用于Paper服务器上的每一个世界，或者调整服务器的某些功能。

## async-chunks

### threads

- **默认值**: `-1`
- **描述**: 服务器应该使用多少线程用于保存世界和加载区块。默认值（-1）将使用服务器线程数量的一半进行区块加载，除非有别的内容规定了此项，并且默认使用最大4个区块用于保存和加载区块。可以使用 `-Dpaper.maxChunkThreads=[数字]` 启动参数进行调整。

## chunk-loading

### autoconfig-send-distance

- **默认**: `true`
- **描述**: 是否要根据客户端设定的可视距离设定作为服务器实际发送给客户端的可视距离。只有此项会设定服务器发送给客户端的区块距离的半径，但是不会影响服务器实际加载和Tick。

### enable-frustum-priority

- **默认值**: `false`
- **描述**: 是否要在加载玩家两侧和后方的区块之前，优先加载玩家前面的区块。由于玩家对此反响并不是很好，所以默认禁用。不建议启用此项。

### global-max-chunk-load-rate

- **默认值**: `-1.0`
- **描述**: 服务器每秒加载区块的最大数值。优先级大于 `player-max-chunk-load-rate`。

### global-max-chunk-send-rate

- **默认值**: `-1.0`
- **描述**: 服务器每秒向客户端发送区块的最大数值。调整此值可能有利于缓解服务器峰值宽带的使用。

### global-max-concurrent-loads

- **默认值**: `500.0`
- **描述**: 服务器每次处理加载区块的最大数值。如果此值超过了`player-max-concurrent-loads`，则覆盖它。

### max-concurrent-sends

- **默认值**: `2`
- **描述**: 每次排队发送区块的最大数值。较低的值会缓解服务器的网络瓶颈，比如使用反矿物透视和压缩。但是此值可能不会如预期的优化网络环境较差的玩家的游戏体验。

### min-load-radius

- **默认值**: `2`
- **描述**: 在区块加载时，玩家周围未造成阻塞的范围（半径）。此值影响的实际范围是设定值+1，并且此项会控制客户端可加载的区块数量。

### player-max-chunk-load-rate

- **默认值**: `-1.0`
- **描述**: 每玩家每秒加载区块的最大数量。

### player-max-concurrent-loads

- **默认值**: `20.0`
- **描述**: 每玩家每次处理区块加载的最大数量。

### target-player-chunk-send-rate

- **默认值**: `100.0`
- **描述**: 每秒钟发送给玩家区块的最大数量。

## collisions

### enable-player-collisions

- **默认值**: `true`
- **描述**: 服务器是否应该开启玩家碰撞。当此项与安装某些影响计分板的插件，可能不起作用。若在调整使用此配置时出现问题，请尝试先禁用这些插件。

### send-full-pos-for-hard-colliding-entities

- **默认值**: `true`
- **描述**: 当与船只或矿车碰撞时，客户端/服务器经常会导致两者在处理时不一致，并使玩家的行为出错。此选项尝试在其发生碰撞时向其发送精确的位置来缓解此问题。开启此选项将消耗更多的带宽，但是在大多数情况下此选项值得开启。

## commands

### fix-target-selector-tag-completion

- **默认值**: `true`
- **描述**: 解决一个客户端Bug，防止实体类型Tag建议在目标选择器中生效。在 [MC-235045](https://bugs.mojang.com/browse/MC-235045) 修复。

### suggest-player-names-when-null-tab-completions

- **默认值**: `true`
- **描述**: 当自动补全无其它参数可用时，将尝试返回Tab列表中的玩家名称。

### time-command-affects-all-worlds

- **默认值**: `false`
- **描述**: 当输入 `/time` 命令时，在所有世界生效还是仅在命令发送者所在的世界生效。

## console

### enable-brigadier-completion

- **默认值**: `true`
- **描述**: 是否要在控制台启用Mojang的命令引擎Brigadier（高级）命令补全。

### enable-brigadier-highlighting

- **默认值**: `true`
- **描述**:  是否要在控制台启用Mojang的命令引擎Brigadier命令高亮。

### has-all-permissions

- **默认值**: `false`
- **描述**: 终端是否默认有全部权限。

## item-validation

### display-name

- **默认值**: `8192`
- **描述**: 物品名称（Display）的最大字符长度。

### lore-line

- **默认值**: `8192`
- **描述**: 物品Lore的最大字符长度。

### resolve-selectors-in-books

- **默认值**: `false`
- **描述** 是否要在书中解析选择器。当启用后，有创造模式的玩家可以用一种方式导致服务器崩溃。

### book

#### author

- **默认值**: `8192`
- **描述**: 书的作者的最大字符长度。

#### pages

- **默认值**: `16384`
- **描述**: 书页数的最大字符长度。

#### title

- **默认值**: `8192`
- **描述**: 书的标题的最大字符长度。

### book-size

#### page-max

- **默认值**: `2560`
- **描述**: 书的单页可以为整书提供的最大字节数。

#### total-multiplier

- **默认值**: `0.98`
- **描述**: 书中单页从最后一页获取的全书最大字节倍数 (第一页的倍数是 `1.0`).

## logging

### deobfuscate-stacktraces

- **默认值**: `true`
- **描述**: 是否将日志中的Spigot mapping堆栈转换为Mojang mapping。该选项对使用Mojang mapping的服务器无效。

### log-player-ip-addresses

- **默认值**: `true`
- **描述**: 服务器日志是否要记录玩家的IP地址。此项的开启与否都不会影响插件获取玩家的IP地址。

### use-rgb-for-named-text-colors

- **默认值**: `true`
- **描述**: ANSI颜色是否应在记录日志时转换为RGB颜色。

## messages

### no-permission

- **默认值**:
  `<red>I'm sorry, but you do not have permission to perform this command. Please contact the server administrators if you believe that this is in error.`
  > 中文参考翻译：`<red>我很抱歉，但是你的权限目前还不能使用此命令。如果你依然认为这是一个错误，请与服务器管理员联系。`
- **描述**: 当玩家权限不足以运行某命令或进行某操作时提示的文本。插件可以为其新增的命令使用不同的提示文本。

### use-display-name-in-quit-messages

- **默认值**: `false`
- **描述**: 当玩家退出服务器时应该用显示名称（可被插件修改，也就是Display name）还是真实的名称。

### kick

#### authentication-servers-down

- **默认值**: `<lang:multiplayer.disconnect.authservers_down>`
- **描述**: 当无法连接到Mojang验证服务器时提示的文本。

#### connection-throttle

- **默认值**: `Connection throttled! Please wait before reconnecting.`
- **默认值**: 当连接阻塞（即点击加入服务器按钮后极快速的断开连接并重新请求加入）时服务器发送给玩家的消息。 可以在 `bukkit.yml` 配置。

#### flying-player

- **默认值**: `<lang:multiplayer.disconnect.flying>`
- **描述**: 当玩家被检测到飞行作弊时踢出服务器显示的消息。

#### flying-vehicle

- **默认值**: `<lang:multiplayer.disconnect.flying>`
- **描述**: 当玩家被检测到驾驶时飞行作弊时踢出服务器显示的消息。

## misc

### fix-entity-position-desync

- **默认值**: `true`
- **描述**: 是否修复服务器与客户端实体同步位置不精确的Bug。修复 [MC-4](https://bugs.mojang.com/browse/MC-4) 的Bug。

### lag-compensate-block-breaking

- **默认值**: `true`
- **描述**: 服务器是否需要使用时间或TPS判断破坏方块时间。客户端视服务器的TPS始终为20，因此将会导致在服务器出现延迟时，破坏方块出现两者不一致的情况。此设置即修复此情况。

### load-permissions-yml-before-plugins

- **默认值**: `true`
- **描述**: 是否要在在加载插件之前优先加载permissions.yml文件，允许在启动时立刻读取其数据。

### max-joins-per-tick

- **默认值**: `3`
- **描述**: 设定每Tick最大多少名玩家允许加入服务器。如果玩家加入时超过了此限制，则会往后推迟加入时间。与 `Bukkit.yml` 配置文件中的 `connection-throttling` 没有任何关系。

### region-file-cache-size

- **默认值**: `256`
- **描述**: 区域文件缓存的最大大小（存储空间）。

### use-alternative-luck-forumula

- **默认值**: `false`
- **描述**: 是否要为幸运效果应用新的 [计算方式](https://gist.github.com/aikar/40281f6c73ec9b6fef7588e6461e1ba9)。同时，未定义但应适用此效果的部分游戏内容也将享受幸运效果。这对钓鱼计算公式有重大变化。

### use-dimension-type-for-custom-spawners

- **默认值**: `false`
- **描述**: 幻翼，流浪商人是否应该在自定义主世界中生成。默认为false为与原版相契合。

## packet-limiter

### all-packets

#### action

- **默认值**: `KICK`
- **描述**:  一旦超过限制时需要采取的处罚措施。当填入 `DROP` 时将忽略超过限制的包，`KICK`将在踢出发送超过限制的包的玩家。

#### interval

- **默认值**: `7.0`
- **描述**: 应用 `max-packet-rate` 时的所需间隔时间，以秒为单位。

#### max-packet-rate

- **默认值**: `500.0`
- **描述**: 一段时间内服务器可接受每名玩家发送最大的包的数量。

### kick-message

- **默认值**: `<red><lang:disconnect.exceeded_packet_rate>`
- **描述**: 玩家发送过多包后踢出服务器时提示的消息。

### overrides

- **默认值**: `ServerboundPlaceRecipePacket`, `DROP`, `4.0`, `5.0`
- **描述**: 为独立命名的任意packet覆盖全局配置。 你可以在Timings找到每一个包的名称。对于有经验的用户，无论什么服务器Packet名均使用Mojang mapping。
<!-- For more information about overrides, see the [Packet Limiter Guide]... -->

## player-auto-save

### max-per-tick

- **默认值**: `-1`
- **描述**: 每Tick最多保存多少名玩家的数据。设定为默认值 `-1` 将会根据 `player-auto-save.rate` 设定一个推荐数值，即`10`或`20`。

### rate

- **默认值**: `-1`
- **描述**: 多少Ticks保存一次玩家数据。如果设定为 `-1` 则会使用 `bukkit.yml` 中的 `ticks-per.autosave` 项。

## proxies

### proxy-protocol

- **默认值**: `false`
- **描述**: 服务器是否需要处理 [代理协议](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt) 消息文本。 这和Velocity或是BungeeCord完全没有关系，仅当你使用HAProxy或类似软件时才应当启用。

### bungee-cord

#### online-mode

- **默认值**: `true`
- **descriptions**: 当服务器作为BungeeCord子端时，该如何处理玩家的UUID和数据。始终保持此项应与BungeeCord设置中的 `online-mode` 一致。

### velocity

#### enabled

- **默认值**: `false`
- **描述**: 是否应该接受 Velocity 的 Modern 协议转发格式。

#### online-mode

- **默认值**: `false`
- **描述**: 当服务器作为Velocity子端时，该如何处理玩家的UUID和数据。始终保持此项应与Velocity设置中的 `online-mode` 一致。

#### secret

- **默认值**: `<空>`
- **描述**: 此服务器和Velocity的Secert字段。 此值必须与Velocity的 `forwarding-secret` 值保持一致。

## scoreboards

### save-empty-scoreboard-teams

- **默认值**: `false`
- **描述**: 许多计分板插件遗漏大量的空的计分板Teams，大大减缓登录速度。是否要自动清理这些无用的计分板Teams。

### track-plugin-scoreboards

- **默认值**: `false`
- **描述**: 服务器是否跟踪计分板插件时只追踪dummy类型的计分项。这是一个突破性的变化，但是默认值`false`是合理的，因为当你使用某些计分板插件时同时启用此项会减缓性能。

## spam-limiter

### incoming-packet-threshold

- **默认值**: `300`
- **描述**: 设定一个阈值。超过此阈值后的所有包都将视为刷屏并忽略它们。

### recipe-spam-increment

- **默认值**: `1`
- **描述**: 当玩家点击一个配方后，配方刷屏计数器应该增加多少数字。

### recipe-spam-limit

- **默认值**: `20`
- **描述**: 配方刷屏计数器应该累计到多少数字后踢出玩家。

### tab-spam-increment

- **默认值**: `1`
- **描述**: 在聊天中按下Tab使用自动补全时，Tab补全刷屏计数器应该增加多少数字。

### tab-spam-limit

- **默认值**: `500`
- **描述**: Tab补全刷屏计数器应该累计到多少数字后踢出玩家。

## timings

### enabled

- **默认值**: `true`
- **描述**: 设定Timings的全局启用状态。

### hidden-config-entries

- **默认值**:
  `[database, settings.bungeecord-address, settings.velocity-support.secret, proxies.velocity.secret]`
- **描述**: 在Timings报告网页上隐藏哪些关于服务器的配置信息。

### history-interval

- **默认值**: `300`
- **描述**: 在Timings报告网页上两个不同的点之间要间隔多长时间。以秒为单位。

### history-length

- **默认值**: `3600`
- **描述**: 单次报告中要保留的数据总量。此值会在Timings服务器上验证，过大的数据会拒绝受理。

### server-name

- **默认值**: `Unknown Server`
- **描述**: Timings中显示的服务器名称是什么。

### server-name-privacy

- **默认值**: `false`
- **描述**: 是否要在Timings报告中隐藏服务器名称相关信息。

### url

- **默认值**: `https://timings.aikar.co`
- **描述**: 指定一个 [Timings Viewer](https://github.com/aikar/timings) 服务器，并将Timings报告发送到该服务器上。

### verbose

- **默认值**: `true`
- **描述**: 是否要在Timings报告中显示更加详细的信息。例如：启用后，某个实体导致服务器卡服，所显示的信息比“实体（entities）”二字要详细的多。

## unsupported-settings

### allow-headless-pistons

- **默认值**: `false`
- **描述**: 是否允许在服务器中出现无头活塞，通常用它来永久破坏正常无法破坏的方块（比如下界破坏基岩天花板）。

### allow-permanent-block-break-exploits

- **默认值**: `false`
- **描述**: 是否可以使用原版漏洞破坏原版“无法破坏”的方块。包含基岩，末地传送门框架，末地传送门等等。

### allow-piston-duplication

- **默认值**: `false`
- **描述**: 是否应该允许破坏TNT，地毯和铁轨。沙子不在此之内。

### perform-username-validation

- **默认值**: `true`
- **默认值**: 服务器是否要验证玩家用户名。如果不启用，则会允许名称中含有特殊字符的玩家加入到服务器，但是会与部分插件不兼容。

## watchdog

### early-warning-delay

- **默认值**: `10000`
- **描述**: 在服务器挂起后，看门狗在多少毫秒后自动崩溃掉服务器。

### early-warning-every

- **默认值**: `5000`
- **描述**: 在服务器挂起后，看门狗在多少毫秒后自动在终端打印线程崩溃时间的间隔。
