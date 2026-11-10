\# Pi Agent 安装与基础使用实践

姓名：谌思雨

学号：202430224066



> 本次实践完成 Pi‑Agent 客户端安装、模型配置会话、模型与思考级别切换、引用代码文件、图片输入、插件安装试用；任务六为选做。所有截图存放在本仓库 `images/` 文件夹。



\## 1 任务一：本地安装并启动 Pi Agent

\### 任务说明

Windows PowerShell执行官方安装命令完成Pi客户端安装，新建项目文件夹并启动pi，验证客户端正常启动，出现版本号，`No models available`代表客户端启动成功，尚未配置模型。



Windows安装命令：

```powershell

powershell -c "irm https://pi.dev/install.ps1 | iex"

```

操作步骤：

1\. 执行安装命令，等待安装完成，关闭旧终端，重新打开PowerShell。

2\. 创建练习目录，进入目录启动pi

```powershell

mkdir pi-test

cd pi-test

pi

```



\*\*截图S1：Pi启动成功截图（包含版本号、工作目录）\*\*

!\[Pi客户端启动成功](images/s1-pi-start.png)



\## 2 任务二：配置模型并完成一次会话

\### 任务说明

采用API‑Key方式登录模型服务商，配置模型，完成一次基础对话会话。

操作步骤：

1\. 前往模型服务商API平台，创建API Key。

2\. 在pi交互终端输入 `/login`，选择`Sign in with an API key`，选择对应模型提供商，粘贴API密钥完成登录。

3\. 发送提示词，验证模型可以正常回复消息。



> ⚠️ 截图不要泄露完整API密钥。



\*\*截图S2：模型配置后基础会话截图\*\*

!\[模型配置与基础会话](images/s2-model-chat.png)



\## 3 任务三：切换模型和模型思考级别

\### 任务说明

切换不同可用模型，同时调整模型思考级别，记录切换前后状态，发送测试提问验证会话可用。

操作步骤：

1\. 使用 `/model`（快捷键`Ctrl+L`）打开模型选择器，记录原有模型，切换为另一个可用模型。发送简短问题验证对话正常。

2\. 使用 `/thinking`（快捷键`Shift+Tab`）切换思考级别，记录切换前后思考级别状态。



> 思考级别仅为推理参数设置，不等于更换模型；部分模型不支持思考级别调整，需要更换支持的模型完成本任务。较高思考级别会增加耗时与token消耗，不代表答案质量一定提升。



\*\*截图S3‑1：切换模型前后状态截图\*\*

!\[模型切换](images/s3‑model‑switch.png)



\*\*截图S3‑2：思考级别切换前后状态截图\*\*

!\[思考级别切换](images/s3‑thinking‑level.png)



\## 4 任务四：@引用代码文件 + 粘贴图片测试

\### 4.1 @引用代码文件

任务说明：在工作目录创建`hello.py`，使用`@`语法引用该代码文件，向AI提问，让AI解析文件内容。



`hello.py`代码内容：

```python

def add(a, b):

&#x20;   return a + b



print(add(2, 3))

```

提示词：

```

请解释 @hello.py 的功能，说明运行后输出什么。只解释，不修改文件。

```



\*\*截图S4：引用代码文件交互截图\*\*

!\[@引用代码文件](images/s4‑at‑code‑file.png)



\### 4.2 粘贴小图片测试

任务说明：准备一张小尺寸测试图片，复制图片到剪贴板，在Pi终端粘贴图片，发送指令让AI识别图片的颜色、形状、数字。

提示词：

```

请描述图片中的颜色、形状和数字。

```



> Windows使用`Alt+V`粘贴图片；如果粘贴异常，用`/hotkeys`查看终端快捷键绑定。



\*\*截图S5：粘贴图片识别交互截图\*\*

!\[粘贴图片识别](images/s5‑paste‑image.png)



\## 5 任务五：自选Pi‑Packages插件安装与试用

\### 任务说明

访问 \[pi.dev/packages](https://pi.dev/packages)，自选一个Pi插件包，执行项目级安装；完全退出Pi会话，重新启动，验证插件在Extensions列表成功加载，调用插件的功能完成测试。



本次选用插件：`pi‑web‑access`

\- 插件作用：提供网页访问、网页内容抓取扩展能力

\- 项目局部安装命令：

```powershell

pi install npm:pi-web-access -l --approve

```

操作流程：

1\. 在项目目录执行插件安装命令。

2\. 完全退出pi，重新执行`pi`启动客户端，观察启动输出`\[Extensions]`区域确认插件加载；也可以执行`pi list`查看已安装包。

3\. 发送测试提示词调用插件功能。

测试提示词：

```

请获取 https://example.com 的页面标题

```



\*\*截图S6‑1：插件安装命令执行输出\*\*

!\[插件安装输出](images/s6‑plugin‑install.png)



\*\*截图S6‑2：重启Pi后Extensions插件加载信息\*\*

!\[插件加载成功](images/s6‑plugin‑loaded.png)



\*\*截图S6‑3：插件功能调用返回结果\*\*

!\[插件功能调用1](images/s6‑plugin‑run1.png)

!\[插件功能调用2](images/s6‑plugin‑run2.png)

!\[插件功能调用3](images/s6‑plugin‑run3.png)



\## 6 任务六：安装PPT Skill（选做）

\### 任务说明

让AI从指定仓库下载pptx skill完整目录，安装到项目目录`.pi/skills/pptx`，验证目录文件完整；退出会话重新启动pi，确认Skill被Pi发现，调用skill命令验证可用性。



提示词发送给Pi Agent：

```

请从 https://github.com/anthropics/skills 下载 skills/pptx 完整目录，安装到当前项目的 .pi/skills/pptx。保留 SKILL.md、LICENSE.txt 和 scripts 等支持文件，记录源 commit。只安装这个 Skill，不修改其他项目，不自动安装依赖；如目标已存在先说明情况。完成后列出目录结构。

```

重新进入pi后调用skill命令：

```

/skill:pptx 请说明这个 Skill 的名称、用途和所在目录

```



\*\*截图S7：pptx skill目录结构截图（展示SKILL.md、LICENSE.txt、scripts文件夹）\*\*

!\[PPT Skill目录结构](images/s7‑skill‑folder.png)



\*\*截图S8：重启Pi后Skill发现与调用结果截图\*\*

!\[PPT Skill调用测试1](images/s8‑skill‑invoke1.png)

!\[PPT Skill调用测试2](images/s8‑skill‑invoke2.png)



\## 实践小结

本次实践完整完成Pi Agent客户端的安装部署，学习了API‑Key方式接入大模型；掌握切换模型、调整思考级别、`@`引用本地代码文件、图片输入、Pi‑package插件安装使用的操作。

实践过程中了解Pi Agent扩展体系：\*\*Extension（插件）用于扩展工具命令；Skill提供任务脚本与业务能力文件\*\*。

操作中遇到部分插件功能受网络、本机环境依赖影响无法完全执行成功；也理解Skill不是npm插件，不能使用`pi install`安装，需要下载完整目录放到项目`.pi/skills`路径下，重启Pi才能被发现加载。通过本次实验，熟悉了终端AI Agent的使用模式与扩展机制。



\---



\# 目录结构要求（本地仓库）

```

pi‑practice‑repo/

├─ README.md        # 这份报告文档

└─ images/          # 全部截图放在这里

&#x20;  ├─ s1‑pi‑start.png

&#x20;  ├─ s2‑model‑chat.png

&#x20;  ├─ s3‑model‑switch.png

&#x20;  ├─ s3‑thinking‑level.png

&#x20;  ├─ s4‑at‑code‑file.png

&#x20;  ├─ s5‑paste‑image.png

&#x20;  ├─ s6‑plugin‑install.png

&#x20;  ├─ s6‑plugin‑loaded.png

&#x20;  ├─ s6‑plugin‑run1.png

&#x20;  ├─ s6‑plugin‑run2.png

&#x20;  ├─ s6‑plugin‑run3.png

&#x20;  ├─ s7‑skill‑folder.png

&#x20;  ├─ s8‑skill‑invoke1.png

&#x20;  └─ s8‑skill‑invoke2.png

```



\# Git提交上传步骤

打开Git Bash，进入仓库根目录

```bash

\# 1.查看变更

git status



\# 2.添加README.md与全部截图

git add README.md images/



\# 3.提交

git commit -m "Pi Agent第一次实践作业：实验报告与全部任务截图"



\# 4.推送到远程main分支

git push origin main

```



> 作业提交要求：上传仓库后，新建issue，issue标题：`实践课1： Pi Agent安装与使用 \[姓名拼音]`，issue内容粘贴仓库README访问链接。



