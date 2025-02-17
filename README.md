<h1 align="center">NoneBot Plugin GsPanel</h1></br>


<p align="center">🤖 用于展示原神游戏内角色展柜数据的 NoneBot2 插件</p></br>


<p align="center">
  <a href="https://github.com/monsterxcn/nonebot-plugin-gspanel/actions">
    <img src="https://img.shields.io/github/workflow/status/monsterxcn/nonebot-plugin-gspanel/Build%20distributions?style=flat-square" alt="actions">
  </a>
  <a href="https://raw.githubusercontent.com/monsterxcn/nonebot-plugin-gspanel/master/LICENSE">
    <img src="https://img.shields.io/github/license/monsterxcn/nonebot-plugin-gspanel?style=flat-square" alt="license">
  </a>
  <a href="https://pypi.python.org/pypi/nonebot-plugin-gspanel">
    <img src="https://img.shields.io/pypi/v/nonebot-plugin-gspanel?style=flat-square" alt="pypi">
  </a>
  <img src="https://img.shields.io/badge/python-3.8+-blue?style=flat-square" alt="python"><br />
</p></br>


| ![琴](https://user-images.githubusercontent.com/22407052/201662130-2b3bdcd3-acaa-4b59-9c88-3e50fa1887f3.PNG) | ![刻晴](https://user-images.githubusercontent.com/22407052/201661930-f9ecdfe0-e278-4641-a012-cf090da6b6c7.PNG) | ![妮露](https://user-images.githubusercontent.com/22407052/201667744-decfdf25-c889-4a65-bbe0-94e194fe8d82.PNG) |
|:--:|:--:|:--:|


## 安装方法


如果你正在使用 2.0.0.beta1 以上版本 NoneBot，推荐使用以下命令安装：


```bash
# 从 nb_cli 安装
python3 -m nb_cli plugin install nonebot-plugin-gspanel

# 或从 PyPI 安装
python3 -m pip install nonebot-plugin-gspanel
```


> **[@realhuhu/py-plugin](https://github.com/realhuhu/py-plugin) 插件用户安装方法**
> 
> Yunzai 用户安装 py-plugin 插件后可以兼容运行此插件！安装步骤如下：
> 
> 1. 仔细阅读 [README.md](https://github.com/realhuhu/py-plugin#21-%E5%AE%89%E8%A3%85) 配置 Yunzai Bot 的 Python 运行环境
> 2. 向 Yunzai Bot 发送 QQ 消息 `#py下载插件nonebot-plugin-gspanel` 安装此插件
> 3. [建议] 将下方使用须知第 4 条中交待的所有环境变量写入 py-plugin 的配置文件 config.yaml 中（注意格式）
> 4. [建议] 将环境变量 `gspanel_alias` 定义为 `面板` 以外的触发词，避免此插件与 Yunzai 相关功能同时触发
> 
> py-plugin 的配置文件 config.yaml 中 **务必手动添加** 此插件的一些配置：
> 
> ```yaml
> gspanel_alias:
>   - 想要的面板触发词
>   - 支持多个触发词
> gspanel_scale: 1.0
> resources_dir: /path/to/data  # Windows 要将反斜杠替换为 /
> resources_mirror: https://enka.network/ui/
> ```


## 使用须知


 - 插件的圣遗物评分计算规则、卡片样式均来自 [@yoimiya-kokomi/miao-plugin](https://github.com/yoimiya-kokomi/miao-plugin)。插件移植时对 **评分规则** 主要做了以下修改：
   
   + 以角色生命值、攻击力、防御力的实际基础值进行词条得分计算，导致固定值的生命值、攻击力、防御力词条评分相较原版有小幅度波动
   + 于面板数据区域展示圣遗物评分使用的词条权重规则，插件尚未自定义词条权重规则的角色使用默认规则（攻击力 `75`、暴击率 `100`、暴击伤害 `100`）
   + 于面板数据区域展示角色最高的伤害加成数据，该属性与角色实际伤害属性不一致时区别显示词条权重规则
   + 对元素属性异常的空之杯进行评分惩罚，扣除该圣遗物总分的 50%（最大扣除比例）
   
 - 插件返回「暂时无法访问面板数据接口..」可能的原因有：Bot 与 [Enka.Network](https://enka.network/) 的连接不稳定；[Enka.Network](https://enka.network/) 服务器暂时故障等。
   
 - 插件首次生成某个角色的面板图片时，会尝试从 [Enka.Network](https://enka.network/) 下载该角色的抽卡大图、命座图片、技能图片、圣遗物及武器图片等素材图片，生成面板图片的时间由 Bot 与 [Enka.Network](https://enka.network/) 的连接质量决定。素材图片下载至本地后将不再从远程下载，生成面板图片的时间将大幅缩短。
   
 - 一般来说，插件安装完成后无需设置环境变量，只需重启 Bot 即可开始使用。你也可以在 NoneBot2 当前使用的 `.env` 文件中添加下表给出的环境变量，对插件进行更多配置。环境变量修改后需要重启 Bot 才能生效。
   
   | 环境变量 | 必需 | 默认 | 说明 |
   |:-------|:----:|:-----|:----|
   | `gspanel_alias` | 否 | `["面板"]` | 插件响应词别名，多个别名按 `["面面", "板板"]` 格式填写 |
   | `gspanel_scale` | 否 | `1.0` | 浏览器缩放比例，此值越大返回图片的分辨率越高 |
   | `resources_dir` | 否 | `/path/to/bot/data/` | 插件数据缓存目录的父文件夹，包含 `gspanel` 文件夹的上级文件夹路径 |
   | `resources_mirror` | 否 | `https://enka.network/ui/` | 素材图片下载镜像，需提供 `UI_Talent_S_Nilou_01.png` 形式的图片地址，可选镜像：<br>`http://file.microgg.cn/ui/`（小灰灰）<br>`https://api.ambr.top/assets/UI/`（安柏计划）<br>`https://cdn.monsterx.cn/genshin/`（插件作者） |
   
 - 插件图片生成采用 [@kexue-z/nonebot-plugin-htmlrender](https://github.com/kexue-z/nonebot-plugin-htmlrender)，若插件自动安装运行 Chromium 所需的额外依赖失败，请参考 [@SK-415/HarukaBot](https://haruka-bot.sk415.icu/faq.html#playwright-%E4%BE%9D%E8%B5%96%E4%B8%8D%E5%85%A8) 给出的以下解决方案：
   
   + Ubuntu：`python3 -m playwright install-deps`
   + CentOS（仅供参考）：`yum install -y atk at-spi2-atk cups-libs libxkbcommon libXcomposite libXdamage libXrandr mesa-libgbm gtk3`
   + 其他非 Ubuntu 系统：[@microsoft/playwright/issues](https://github.com/microsoft/playwright/issues)


## 命令说明


### 角色面板


插件响应以 `#panel` / `#面板` 开头的消息，下面仅以 `#面板` 为例：


*\*如果定义了环境变量 `gspanel_alias` 则以环境变量定义的命令别名为准，默认情况下该环境变量会使插件响应 `#面板` 开头的消息。*


 - `#面板绑定100123456`
   
   绑定 UID `100123456` 至发送此指令的 QQ，QQ 已被绑定过则会更新绑定的 UID。
   
   Bot 管理员可以通过在此指令后附带 `@某人` 或 `2334556789` 的方式将 UID `100123456` 绑定至指定的 QQ。
   
 - `#面板100123456`
   
   查找 UID `100123456` 角色展柜中展示的所有角色（文本）。
   
   仅发送 `#面板` 时将尝试使用发送此指令的 QQ 绑定的 UID；发送 `#面板@某人` 时将尝试使用指定 QQ 绑定的 UID。
   
 - `#面板夜兰100123456` / `面板100123456夜兰`
   
   查找 UID `100123456` 的夜兰面板（图片）。
   
   仅发送 `#面板夜兰` 时将尝试使用发送此指令的 QQ 绑定的 UID；发送 `#面板夜兰@某人` 时将尝试使用指定 QQ 绑定的 UID。


*\* 所有指令都可以用空格将关键词分割开来，如果你喜欢的话。*


### 队伍伤害


插件响应以 `#teamdmg` / `#队伍伤害` 开头的消息，下面仅以 `#队伍伤害` 为例：


 - `#队伍伤害` / `#队伍伤害100123456` / `#队伍伤害@某人`
   
   查找指定 UID 角色展柜中前四个角色组成的队伍伤害。
   
   当仅发送 `#队伍伤害` 时将尝试使用发送此指令的 QQ 绑定的 UID；附带 9 位数字时尝试使用该 UID；附带 `@某人` 时将尝试使用指定 QQ 绑定的 UID。
   
 - `#队伍伤害雷九万班` / `#队伍伤害 雷神 九条 万叶 班尼特` / `#队伍伤害雷神 九条 万叶 班尼特@某人`
   
   查找雷电将军、九条裟罗、枫原万叶、班尼特组成的队伍伤害。注意角色名之间必须使用空格分开。含有 **旅行者** 的配队暂时无法查询。
   
   为此形式的命令指定 UID 方式与上面相同。
   
   队伍别名支持可能不全请见谅，如果有十分流行的配队未能支持请提出 issue 耐心等待适配。


*\* 队伍伤害为 **实验性功能**，计算结果可能存在问题。欢迎附带详细日志提交 issue 帮助改进此功能。*


## 特别鸣谢


[@nonebot/nonebot2](https://github.com/nonebot/nonebot2/) | [@Mrs4s/go-cqhttp](https://github.com/Mrs4s/go-cqhttp) | [@yoimiya-kokomi/miao-plugin](https://github.com/yoimiya-kokomi/miao-plugin) | [Enka.Network](https://enka.network/) | [Miniprogram Teyvat Helper](#)
