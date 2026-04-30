# macOS App 启动器制作指南

本指南教你用 macOS 自带的"自动操作"工具把 AirplaneAI 打包成一个可以双击启动的 App。

## 准备工作

先把 AirplaneAI 文件夹放在你的用户目录下：

1. 打开访达，按 `Shift + Cmd + H` 进入用户目录
2. 把 `airplane-ai` 文件夹拖进去
3. 确认路径为 `/Users/你的用户名/airplane-ai`

## 制作 App

### 步骤一：打开自动操作
1. 在启动台中搜索 **"自动操作"**（英文系统搜 **Automator**）
2. 点击"新建文稿"
3. 选择"应用程序"类型，点击"选取"

### 步骤二：添加启动命令
1. 在左侧搜索框中搜索"运行 Shell 脚本"
2. 将"运行 Shell 脚本"拖到右侧空白区域
3. 把下面的内容粘贴到文本框中：

```
/usr/bin/python3 "$HOME/airplane-ai/scripts/offline_chat.py" \
  --llm-url "http://127.0.0.1:1234/v1/chat/completions"
```

不需要写 `pkill` 或 `nohup`，自动操作会自动管理进程。

### 步骤三：保存
1. 按 `Cmd + S` 保存
2. 名称写"断网应急聊天"
3. 位置选"应用程序"或桌面
4. 关闭自动操作

## 启动

使用前请确保 LM Studio 已经加载模型并开启了 Local Server。

双击你刚保存的 App 即可启动。浏览器会自动打开 `http://127.0.0.1:8765`。

如果浏览器没有自动打开，手动在浏览器输入 `http://127.0.0.1:8765`。

## 自定义

- 如果 LLM 用的不是 LM Studio 默认端口（1234），修改命令里的 `--llm-url` 地址
- 如果想自定义 AI 风格，在命令里加 `--persona-file` 参数并指向你的人设文件
- 模型名会自动探测，一般不需要手动指定
