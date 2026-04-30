# macOS .app launcher for AirplaneAI

## 准备工作
先把 AirplaneAI 文件夹放在你方便的地方，比如：
```
~/airplane-ai
```

## 制作 .app
1. 打开 **Automator** → 新建文稿 → **应用程序**
2. 搜索并添加 **"运行 Shell 脚本"** 操作
3. 粘贴下面的脚本
4. 保存为 `AirplaneAI.app` 到桌面或应用程序文件夹

```bash
#!/bin/bash
SCRIPT_DIR="$HOME/airplane-ai"
cd "$SCRIPT_DIR"

# 关掉已有实例
pkill -f "offline_chat.py" 2>/dev/null
sleep 1

# 启动（自动探测模型名，无需手动指定）
nohup /usr/bin/python3 "$SCRIPT_DIR/scripts/offline_chat.py" \
  --llm-url "http://127.0.0.1:1234/v1/chat/completions" \
  > /tmp/airplane-ai.log 2>&1 &

sleep 2
open "http://127.0.0.1:8765"
```

## 自定义
- 如果你的 LLM 用的不是 LM Studio 默认端口，改 `--llm-url` 即可
- 如果想自定义 AI 性格，加 `--persona-file "$SCRIPT_DIR/persona.txt"`
- 模型名会自动探测，一般不需要写

## 使用
1. 打开 LM Studio → 加载模型 → 开启 Local Server
2. 双击 `AirplaneAI.app`
3. 浏览器自动打开，开始聊天
