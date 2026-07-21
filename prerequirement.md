# Prerequisites

完成本仓库所有 Lab 所需的软件与账号。

## 账号

| 账号 | 用途 | 涉及 Lab |
|------|------|----------|
| GitHub | 托管 gh-aw 工作流与 GitHub Actions | Lab-01 |
| DeepSeek（含 API 余额） | DeepSeek API Key 与模型调用 | Lab-01 |

## 软件

| 软件 | 最低版本 | 涉及 Lab | 安装 |
|------|---------|----------|------|
| Git | 2.x | 全部 | https://git-scm.com |
| GitHub CLI (`gh`) | 2.x | 全部 | https://cli.github.com |
| gh-aw 扩展 | latest | Lab-01 | `gh extension install github/gh-aw` |
| Python | 3.11+ | 全部 | https://www.python.org |
| Node.js | 24+ | 全部 | https://nodejs.org |
| VS Code | latest | 全部（推荐） | https://code.visualstudio.com |

## 快速验证

```bash
git --version          # >= 2.x
gh --version           # >= 2.x
gh aw --version        # 已安装即可
python3 --version      # >= 3.11
node --version         # >= 24
code --version         # 已安装即可
```
