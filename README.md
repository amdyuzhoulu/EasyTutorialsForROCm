
 # ROCm 简明教程（EasyTutorialsForROCm）

本文档旨在帮助中国地区的教师和学生更顺利地上手 ROCm 软件栈。

---

# 基础硬件信息

建议使用支持 AMD ROCm 的 iGPU AIPC（集成显卡处理器）和 RDNA3/RDNA4 架构的 dGPU（独立显卡）。以下是一些推荐设备示例：

1. **集成显卡（iGPU）**：Strix（370、375）、Strix-Halo（395）、Pheonix（7940、7640）
2. **独立显卡（dGPU）**：RDNA3（7900XTX、7900XT、7900GRE、W7900），RDNA4（9070XT、9060XT）

这些设备在 ROCm 软件中得到了一定程度的支持，iGPU 设备（Strix、Strix-Halo、Pheonix）需要添加额外的环境变量配置，例如：

```
env: 
  - name: HSA_OVERRIDE_GFX_VERSION
    value: "11.0.0"
```

请确保所有设备均可连接完整可用的互联网。

---

# 基础软件环境配置

请安装 **Ubuntu 24.04.2 LTS** 操作系统，并使用 **6.11 版本内核**。请注意：

* 安装完成后 **锁定内核版本为 6.11**。
* **不要运行 `apt upgrade` 命令**，以避免内核自动升级至 6.14。

否则可能会导致与 ROCm 不兼容的问题。

---

# 基础 BIOS 设置


