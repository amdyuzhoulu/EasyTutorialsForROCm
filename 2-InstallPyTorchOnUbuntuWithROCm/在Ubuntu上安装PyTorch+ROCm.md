

# 在 Ubuntu 24.04.2 + ROCm 环境下安装 PyTorch

---

## ✅ 必要条件确认

在开始前，请确保系统满足以下条件：

* [x] 操作系统：Ubuntu 24.04.2 LTS
* [x] 内核版本：**6.11**（不可为 6.14 及以上）
* [x] ROCm 已正确安装，`rocm-smi` 和 `rocminfo` 可正常输出
* [x] 已连接网络，可访问 PyTorch 和 ROCm 的官方镜像源

---

## 🎯 本节目标

* 安装 Anaconda 或 Mamba（UV）作为 Python 包管理器
* 创建独立环境并安装 PyTorch（带 ROCm 支持）
* 运行示例程序测试 PyTorch 是否能识别 AMD GPU
* （可选）扩展：安装 Transformers、Dataloader 测试等

---

## 📦 步骤 1：安装 Anaconda / Mamba（UV）

推荐使用轻量级的 Conda 替代品 **Mamba（uv）**，安装更快。你也可以选择官方 Anaconda。

### 方式一：安装 Anaconda

```bash
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh
bash Anaconda3-2024.02-1-Linux-x86_64.sh
```

安装完成后运行：

```bash
source ~/.bashrc
conda --version
```

---

### 方式二（推荐）：安装 Mamba (conda + UV)

```bash
curl -Ls https://micro.mamba.pm/api/micromamba/linux-64/latest | tar -xvj bin/micromamba
mkdir -p ~/mambaforge
./bin/micromamba shell init -s bash -p ~/mambaforge
source ~/.bashrc
micromamba create -n torch-rocm python=3.10 -y
micromamba activate torch-rocm
```

---

## 🔧 步骤 2：安装 PyTorch（ROCm 版）

参考 AMD 官方提供的 PyTorch ROCm wheel：

### 安装命令（适用于 ROCm 6.4.x + Python 3.1*）：

```bash
pip3 install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.4
```




### 安装命令（适用于 ROCm 6.3.x + Python 3.1*）：

```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/rocm6.3
```

> 若提示找不到 wheel，请确保你的 Python 是 3.10+ 且平台为 x86\_64。


---

## ✅ 步骤 3：验证 GPU 是否可用

运行以下 Python 脚本：

```python
import torch

print("PyTorch version:", torch.__version__)
print("ROCm available:", torch.version.hip)
print("Is ROCm GPU available:", torch.cuda.is_available())
print("Device count:", torch.cuda.device_count())
print("Current device:", torch.cuda.current_device())
print("Device name:", torch.cuda.get_device_name(0))
```

### 预期输出示例（AI MAX 395）：

```
PyTorch version: 2.3.0+rocm6.4
ROCm available: True
Is ROCm GPU available: True
Device count: 1
Current device: 0
Device name: AMD Radeon Graphics (gfx1100)
```

若能正确识别出 gfx1100 等设备，即表示安装成功。

---

## 📚 扩展内容（可选）

### 1. 安装 Transformers 等深度学习库

```bash
pip install transformers accelerate tqdm
```

### 2. 运行推理测试

```python
from transformers import pipeline

pipe = pipeline("text-generation", model="EleutherAI/gpt-neo-125M", device=0)
print(pipe("Hello, I'm using ROCm", max_length=30))
```

（若模型不支持 ROCm，会 fallback 到 CPU）

---

## 📌 小结

你现在已经成功：

* 安装 Python 包管理器（Conda / Mamba）
* 安装并验证 ROCm 版本的 PyTorch
* 成功运行基础推理程序

如需在 JupyterLab、Docker 或多 GPU 系统中使用 PyTorch + ROCm，我可以继续为你提供详细配置教程。是否继续？
