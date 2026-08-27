# PyTorch-Conda-CUDA-Setup
Windows 下使用 Miniconda 创建独立环境，安装支持 CUDA 11.8 的 PyTorch（含 torchvision、torchaudio），并配置 PyCharm 使用该环境的完整教程。适用于 RTX 30 系列显卡（3060/3080 等）。
# PyTorch Conda CUDA Setup Guide (Windows)

完整教程：在 Windows 上使用 **Miniconda** 创建独立环境，安装支持 **CUDA 11.8** 的 PyTorch，并配置 PyCharm 使用该环境。

适用于 RTX 3060 / 3080 等 30 系列显卡。

---

## 环境信息

| 项目 | 版本 |
|------|------|
| Python | 3.11 |
| PyTorch | 2.5.1 |
| CUDA | 11.8 |
| 操作系统 | Windows 10 / 11 |
| 显卡测试 | RTX 3060 12G（后续可无缝升级到 3080） |

---

## 一、前置准备

1. 安装 [Miniconda](https://docs.conda.io/en/latest/miniconda.html)（推荐）或 Anaconda
2. 安装最新 NVIDIA 显卡驱动
3. 打开 **Anaconda Prompt** 或 **PowerShell**

---

## 二、创建并安装环境

### 1. 接受 Anaconda 服务条款（首次使用需要）

```bash
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/msys2

2. 创建环境
```bash
Bashconda create -n pytorch118 python=3.11 -y
3. 激活环境
```bash
Bashconda activate pytorch118
4. 安装 PyTorch（CUDA 11.8）
```bash
Bashconda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia -y

三、验证安装
在已激活的环境中运行：
```bash
Bashpython -c "import torch; print(torch.__version__); print(torch.cuda.is_available()); print(torch.cuda.get_device_name(0))"
正常输出示例：
text2.5.1
True
NVIDIA GeForce RTX 3060

四、配置 PyCharm 使用该环境

打开 PyCharm → 打开或新建项目
点击右下角解释器 → Add New Interpreter → Add Local Interpreter
选择 Conda Environment → Use existing environment
选择 pytorch118
点击 OK

之后右下角会显示 pytorch118，即可正常编写和运行代码。

五、常用命令
Bash# 激活环境
```bash
conda activate pytorch118

# 退出环境
```bash
conda deactivate

# 查看已安装包
```bash
conda list

# 删除环境（如果需要）
```bash
conda remove -n pytorch118 --all

六、注意事项

本环境使用 CUDA 11.8，兼容 RTX 30 系列显卡（3060 / 3070 / 3080 等）
更换显卡（如升级到 3080）后，只要驱动正常，无需重新安装环境
推荐 Python 3.11，兼容性最好
安装过程中如果提示 Terms of Service，执行上面的 conda tos accept 命令即可


七、快速复现命令汇总
```bash
Bashconda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/main
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/r
conda tos accept --override-channels --channel https://repo.anaconda.com/pkgs/msys2

conda create -n pytorch118 python=3.11 -y
conda activate pytorch118
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia -y

作者：根据实际安装过程整理

最后更新：2026-08
text
