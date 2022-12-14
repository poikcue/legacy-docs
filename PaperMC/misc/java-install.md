
# 安装或更新Java 

安装Java是Paper，Velocity和Waterfall运行或开发插件所需最重要的一步。  
该指南将会指导在主流平台上关于安装Java的推荐步骤。

> **不要使用Headless的Java版本**  
> Java的`headless`版本在其包名后通常带有`-headless`后缀。该`headless`版本缺少运行Paper的必要依赖项，因此不推荐使用。

> **选择Java**  
>  本指南将重点说明亚马逊的Corretto OpenJDK发行版。因为它在大多平台提供最佳安装体验。不过，Corretto不是唯一一个可以使用的OpenJDK版本。你可以选择许多OpenJDK，比如[Eclipse Adoptium](https://adoptium.net/)，[Microsoft](https://www.microsoft.com/openjdk)以及[Azul Zulu](https://www.azul.com/downloads/?package=jdk)等等。  
>  注意：虽然Oracle提供的JDK发行版与它们的功能是一致的，但是由于相当不友好的安装工具和其有恶意许可证的历史而**不推荐**使用。

## Linux

### Ubuntu/Debian

在基于 Debian 系统的Linux发行版上安装Java17很简单。首先，需要确保你的服务器系统有所有安装Java所需的工具。

```bash
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install software-properties-common ca-certificates apt-transport-https curl
```

接下来，导入Amazon Corretto公钥和adpt存储库。

```bash
curl https://apt.corretto.aws/corretto.key | sudo apt-key add -
sudo add-apt-repository 'deb https://apt.corretto.aws stable main'
```

然后安装Java17。

```bash
sudo apt-get update
sudo apt-get install -y java-17-amazon-corretto-jdk
```

现在，请跳转到 [验证安装](#验证安装) 确认是否安装成功。

### 基于 RPM

要在CentOS，RHEL，openSUSE，SLES或任何基于RPM的Linux发行版上安装Java17，请选择服务器使用的包管理器然后选择对应命令。当安装完成后，请跳转到 [验证安装](#verifying-installation) 确认是否安装成功。

#### DNF

在Fedora，CentOS/RHEL 7+及任何与其相关的发行版上使用DNF。

```bash
sudo rpm --import https://yum.corretto.aws/corretto.key
sudo curl -Lo /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo
sudo dnf -y install java-17-amazon-corretto-devel
```

#### Zypper

在openSUSE，SLES及任何相关发行版上使用Zypper。

```bash
sudo zypper addrepo https://yum.corretto.aws/corretto.repo
sudo zypper refresh
sudo zypper install java-17-amazon-corretto-devel
```

#### YUM

在CentOS/RHEL的旧版本，和过老的Fedora版本上使用YUM。

```bash
sudo rpm --import https://yum.corretto.aws/corretto.key
sudo curl -Lo /etc/yum.repos.d/corretto.repo https://yum.corretto.aws/corretto.repo
sudo yum -y install java-17-amazon-corretto-devel
```

## Windows 10 & 11

如果你正在使用Windows 10或11，安装Java就如安装其它软件一样简单。只需从[官方网站](https://corretto.aws/downloads/latest/amazon-corretto-17-x64-windows-jdk.msi)下载Amazon Corretto安装包，然后运行。  
当你使用安装包时，全程点击"next"都是安全的，不会安装任何捆绑，并且全部功能都开箱即用的。

当安装完成后，打开命令提示符并跳转到 [验证安装](#验证安装) 确认是否安装成功。

## macOS/OS X

如果你正在使用macOS，安装Java最佳的方式是使用一个叫做[Homebrew](https://brew.sh)的工具。遵循它们的官网说明，然后安装它。  
接下来，打开你的终端然后运行下列命令：

```bash
brew install openjdk@17
```

当运行命令完成后，跳转到 [验证安装](#验证安装) 确认是否安装成功。  

## Pterodactyl
*（译者没有用过。好像是翼龙面板。）*

> **注意！**    
> 若正在使用低于 `1.2.0` 的Pterodactyl版本，则需要使用管理员账户才能更改Java版本。因此，下述内容将无效。

如果你使用不支持的Java版本启动Paper服务器，Pterodactyl 会自动提示你需要升级Java。就像是这样：

![Pterodactyl Automatic Prompt](https://docs.papermc.io/assets/images/pterodactyl-prompt-08eaa04490182b153a7e203d414da64b.png)

如果该没有显示该弹窗，那么Java版本就意味着可以手动更改。转到服务器 `Startup` 一栏，如下图一样，在"Docker Image"中选择 `ghcr.io/pterodactyl/yolks:java_17`。

![Pterodactyl Manual Java Version Change](https://docs.papermc.io/assets/images/pterodactyl-manual-59004882b8766e775ceefd62de2cbc50.png)

验证安装在Pterodactyl上将无效。

## 验证安装

现在你应该成功地安装了Java17。在你的终端运行下列命令确保成功安装。

```bash
java -version
```

.输出应该像下列文本。最重要的是需要以 `openjdk 17` 开头并在尾行包含 `64-Bit`。如果输出类似于 `java: command not found`，则尝试在使用新的终端会话后重试。

```
openjdk 17 2021-09-14 LTS
OpenJDK Runtime Environment Corretto-17.0.0.35.1 (build 17+35-LTS)
OpenJDK 64-Bit Server VM Corretto-17.0.0.35.1 (build 17+35-LTS, mixed mode, sharing)
```

若安装失败，请不要犹豫，立即在我们的 [Discord](https://discord.gg/papermc) 的`#paper-help`频道中寻求帮助。
