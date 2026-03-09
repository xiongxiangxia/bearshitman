1.1 实验目的
>
掌握aarch64环境下OpenClaw服务搭建

Ps. 本实验强烈建议您点击右上角的下载按钮，下载原版指导书后进行实验。

1.2 环境信息
>
本次上机实验所使用环境信息
通算虚拟机# 操作系统&内核版本Ubuntu 24.04 LTS (GNU/Linux 6.8.0-31-generic aarch64) # Python版本Python 3.8.2 # Node.js版本Node v22.22.0
1.3 实验步骤
>
1.3.1 拉起OpenClaw服务
使用MobaXterm登录服务器

# 使用桌面上MobaXTerm连接您所分配到的服务器，您所分配到的服务器IP&账号&密码在浏览器右侧。

 

检查OpenClaw是否已经安装

输入以下命令检查OpenClaw是否已经安装, 若回显如下则证明OpenClaw已安装，请参考附录中3.1.1实验设备快照恢复，将服务器恢复为原始状态后继续进行实验。

# openclaw doctor



安装nvm工具

# export http_proxy="http://171.60.1.100:7890"

# export https_proxy="http://171.60.1.100:7890"

# curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# source ~/.bashrc



说明：1. nvm工具托管在github，如遇网络波动导致无法下载仓库，可等待3-5分钟之后再试。

2. nvm是一个用于管理Node.js版本的工具，亦可以用来下载和安装Node.js。

安装Node.js

# nvm install 22

# nvm use 22



说明：1. Node.js是一个基于ChromeV8引擎的JavaScript运行环境。Node.js使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。简单的说Node.js就是运行在服务端的JavaScript。

安装&配置OpenClaw依赖

# curl -fsSL https://openclaw.ai/install.sh | bash



说明：1. 安装过程持续大概15-20分钟。

1.3.2 配置OpenClaw服务
OnBoarding配置

1. 风险声明选择Yes

2. Onboarding Mode选择 QuickStart

3. Model/auth Provider选择Qwen（Qwen对于新注册用户，每个模型赠送100万Token余额）


4. 选择Qwen Oauth模式后将显示Oauth网址，复制该网址到浏览器中打开。


5. 确认登录qwen-code后返回ssh终端（若无qwen账号，请自行注册）


6. Default Model选择Keep current

7. Select channel选择Skip for now

8. Configure skills now 选择No

9. Enable hooks选择Skip for now(在该步骤需使用空格键先选定，再回车键确认)

10. How do you want to hatch your bot 选择 Do This Later

配置SSH转发隧道

Win+R快捷键打开跳板机上cmd工具并输入以下命令，并输入服务器root密码，输入后保持cmd在后台运行。

# ssh -N -L 18789:127.0.0.1:18789 root@{你的服务器IP}

例如你的服务器IP为168.17.100.141则命令为

# ssh -N -L 18789:127.0.0.1:18789 root@168.17.100.141


1.3.3 访问OpenClaw服务
访问OpenClaw服务

在配置历史中找到Control UI项，并复制其中Web UI(with token)，并在浏览器中打开


在对话框中输入test，查看是否有返回结果。


2 应用OpenClaw
>
2.1 实验目的
>
掌握使用OpenClaw进行服务器运维

掌握OpenClaw Skills配置

PS. 本章节为抛砖引玉，带领您了解OpenClaw可应用的场景。您也可以自由发挥，使用

OpenClaw完成您需要做的工作

2.2 环境信息
>
基于章节1搭建的OpenClaw服务

2.3 实验步骤
>
2.3.1 OpenClaw进行服务器运维
测试网段内服务器连通性

在对话框中输入以下内容：

请测试一下171.58.2.x/24 网段的连通性，并测试在该网段下有多少个IP可以ping通。测试完毕后请生成一个测试报告在root目录下。



等待OpenClaw完成任务后，检查root目录下是否生成了测试报告。

 

定时任务编写

在对话框中输入以下内容：

请在/root目录下创建test文件夹，并编写定时任务，每10s在该文件夹下创建一个文件，文件名称为创建该文件的时间，定时任务持续10分钟。

 

2.3.2 OpenClaw部署Github开源项目
部署Open-Notebook

在对话框中输入以下内容：

请基于指导文档，在本机部署一个Open Notebook服务，请先使用apt-get install docker.io命令在本地安装好docker，apt-get install docker-compose安装docker-compose服务之后再拉取镜像，若镜像拉取失败，可尝试使用docker.1ms.run。


若单次对话OpenClaw未完成任务，可要求其进行重试。

2.3.3 OpenClaw Skills配置
安装Skills

# mkdir -p ~/.openclaw/workspace/skills

# mkdir -p /home/nas

# apt-get install nfs-common -y

# mount 171.37.2.8:/share /home/nas

# cp -r /home/nas/weifulun/openclaw/xlsx ~/.openclaw/workspace/skills/

测试Skills

在对话框中输入以下内容:

请使用~/.openclaw/workspace/skills/xlsx skills在root目录下创建一个excel文件，其中表头为姓名、年龄，第一行内容为雨姐、18。

 
2.3.4 环境清理
参考3.1.1章节，进行实验环境还原

3 附录
>
3.1 常见操作
>
3.1.1 实验设备快照恢复
下载快照恢复工具

打开跳转机上文件管理器，进入FileShare_TSD盘，依次进入04-Ascend\OpenClaw在线实验工具目录，将resume_openclaw_vm.exe下载至跳转机桌面上


使用快照恢复工具

双机打开resume_openclaw_vm.exe工具，按照以下步骤恢复虚拟机快照

1. 输入虚拟机IP

2. 点击查找快照

3. 选择init快照

4. 点击恢复快照

等待约3分钟后，快照恢复完毕。

