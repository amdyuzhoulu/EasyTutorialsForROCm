

# 在 Ubuntu 上安装 Docker 并运行 ROCm 镜像

## 🧩 开始前你需要确保：

* ✅ 操作系统为 **Ubuntu 24.04.2**
* ✅ 内核版本为 **6.11**
* ✅ 已成功安装 **ROCm**
* ✅ `rocm-smi` 命令可正常运行，能检测到 GPU 状态
* ✅ 拥有 **sudo 权限**
* ✅ 能够连接到 `docker.io`（Docker Hub 网络）
* ✅ 当前系统中 **未安装 Docker** 或已完全卸载旧版本

---

## 🎯 本节完成后你将能够：

* 成功安装 Docker 并完成基础配置
* 拉取并运行 ROCm 官方开发镜像
* 在容器中运行 `rocm-smi` 等 ROCm 命令

---

## 步骤 1：安装 Docker

Docker 官方提供了一键安装脚本，推荐使用以下命令完成安装：

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

> 如需预演（不实际安装），可加上 `--dry-run`：
>
> ```bash
> sudo sh ./get-docker.sh --dry-run
> ```

详细参考：[Docker 官方安装文档](https://docs.docker.com/engine/install/ubuntu/)

---

## 步骤 2：将当前用户加入 docker 用户组（可选）

默认情况下，`docker` 命令需要 `sudo`。如果希望当前用户能直接运行 Docker 命令，可执行以下操作：

```bash
sudo groupadd docker        # 如果 docker 组已存在会提示已存在，无需处理
sudo usermod -aG docker $USER
newgrp docker                # 刷新用户组（当前终端会话生效）
```

> 注：执行完上述命令后，建议 **重新登录系统** 或重新打开终端。

---

## 步骤 3：验证 Docker 是否安装成功

```bash
docker run hello-world
```

若输出类似 “Hello from Docker!” 即表示安装成功。

---

## 步骤 4：（可选）设置 Docker 开机自动启动

```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

---

## 步骤 5：拉取并运行 ROCm 开发测试镜像

ROCm 团队维护了一个专用于开发和测试的官方容器镜像。

### 拉取镜像：

```bash
sudo docker pull rocm/rocm-terminal
```

### 运行容器：

```bash
sudo docker run -it \
  --device=/dev/kfd \
  --device=/dev/dri \
  --security-opt seccomp=unconfined \
  --group-add video \
  rocm/rocm-terminal
```

---

## 步骤 6：验证容器内 ROCm 是否可用

进入容器后，执行：

```bash
rocm-smi
```

如果能看到 GPU 列表（如 gfx1100、gfx1036 等）及其状态，说明 ROCm 环境已在容器中成功加载。

---

## 🔚 总结

你现在已经完成：

* Docker 安装与配置
* ROCm 开发容器的启动与验证


