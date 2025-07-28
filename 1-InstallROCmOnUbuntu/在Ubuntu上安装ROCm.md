

# 开始使用 ROCm（适用于 Ubuntu 24.04.2 + Strix/Phoenix 系列 iGPU）

## ✅ 系统要求

* **操作系统**：Ubuntu 24.04.2 LTS
* **内核版本**：必须固定为 `6.11`，**切勿升级到 6.14 或更高版本**，否则可能导致 ROCm 无法正常工作。
* **支持的 APU（iGPU）平台**：

  * **Strix** 系列（如 370、375）
  * **Phoenix** 系列（如 7640、7940）
  * **Strix-Halo** 系列（如 395）

---

## 🎯 完成本章节你将能够：

* 安装 ROCm 6.4.1 或 6.4.2 并完成环境配置
* 学习使用基本 ROCm 工具和命令
* （可选）安装常用的 ROCm 社区可视化工具，辅助调试 GPU 使用情况

---

## 🛠️ 安装方式

### 方法一：参考官方教程安装（适合高级用户，需 `sudo` 权限）

ROCm 官方文档提供了详细的安装步骤：
🔗 [ROCm 官方安装指南](https://rocm.docs.amd.com/projects/install-on-linux/en/latest/)

注意事项：

* 请严格按照 Ubuntu 24.04 的说明操作
* 安装前需确认内核版本是否为 `6.11`

---

### 方法二：（推荐）使用一键脚本安装（需 `sudo` 权限）

我们提供了为不同 Ubuntu / ROCm 版本预设好的自动化安装脚本，能快速完成所有必要步骤。

1. 克隆对应的安装脚本仓库（确保网络畅通）：

   ```bash
   git clone https://github.com/amdyuzhoulu/rocm-install-script.git
   ```
2. 选择对应版本分支并pull

3. 进入脚本目录并运行主安装脚本：

   ```bash
   cd rocm-install-script
   sudo bash 2-install.sh
   ```

脚本将自动完成 ROCm 软件源配置、依赖项安装以及 ROCm 核心组件部署。

---

## ✅ 安装验证

安装完成后，可以使用以下命令检查系统中的 ROCm 是否正常工作：

### 1. 查看显卡状态和实时使用情况：

```bash
rocm-smi
```

输出信息包括 GPU 温度、频率、使用率等状态。

### 2. 查看系统中已识别的 GPU 设备信息：

```bash
rocminfo
```

若输出包含 `gfx1100` 或其他 iGPU 设备，说明识别成功。

---

## 🧰 额外推荐工具：`amdgpu_top` （图形化命令行工具）

`amdgpu_top` 是一款社区维护的实用工具，用于实时监控 AMD GPU 使用状态，类似于 `htop` 的界面。

### 安装方式：

```bash
wget https://github.com/Umio-Yasuno/amdgpu_top/releases/download/v0.10.5/amdgpu-top_0.10.5-1_amd64.deb
sudo apt install ./amdgpu-top_0.10.5-1_amd64.deb
```

### 使用方法：

```bash
amdgpu_top
```

在终端中即可看到图形化的 GPU 使用监控界面，支持查看显存、频率、利用率等核心信息。

