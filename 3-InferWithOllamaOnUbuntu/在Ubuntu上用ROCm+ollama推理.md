好的，以下是根据你提供的正确安装命令，**适用于 Ubuntu 24.04.2 + ROCm + AMD GPU 的 Ollama 安装与使用指南**：

---

## ✅ 前提条件

确保以下条件满足：

* 操作系统：**Ubuntu 24.04.2 LTS**
* 内核版本：**6.11.x**
* GPU 驱动：**ROCm >= 6.4** 已正确安装
* 显卡支持 ROCm（如 7900XTX、7900GRE、Strix APU 等）
* 环境变量设置：

  ```bash
  export HSA_OVERRIDE_GFX_VERSION=11.0.0
  ```

---

## 🛠 安装 Ollama

### 1. 使用官方安装脚本（推荐方式）

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

该命令会自动下载并安装 `ollama` 到 `/usr/local/bin/ollama`，同时启动后台服务。

### 2. 启动服务（如未自动启动）

```bash
ollama run deepseek-r1
```

你可以在终端中运行互动推理命令。

---

