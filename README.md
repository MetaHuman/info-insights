# EV Tech Insights

基于 GitHub Agentic Workflows 与 DeepSeek API 的电动车行业洞察流水线。

项目从多个 EV 行业 RSS 信号源抓取内容，完成热点聚类、市场洞察和 Markdown 报告生成，并可通过 GitHub Pages 展示最新报告。

## 工作流程

```text
RSS 信号源
  → 抓取与清洗
  → DeepSeek 热点聚类
  → DeepSeek 洞察生成
  → Markdown 报告
  → Pull Request
  → GitHub Pages
```

AI 模型使用 `deepseek-v4-flash`。工作流通过 gh-aw 的 BYOK 配置调用 DeepSeek OpenAI 兼容接口，不要求 GitHub Copilot 订阅。

## 项目结构

```text
.
├── .github/workflows/
│   ├── tech-insight.md          # gh-aw 工作流源文件
│   ├── tech-insight.lock.yml    # 编译后的 GitHub Actions 工作流
│   └── deploy-pages.yml         # GitHub Pages 部署
└── Lab-01-Tech-Insights/
    ├── input/api/               # RSS 数据源配置
    ├── mcp-scripts/             # 抓取、聚类、洞察与报告工具
    ├── output/                  # 流水线输出
    ├── frontend/                # 报告展示页面
    ├── run_local_pipeline.py    # 本地 fallback 诊断脚本
    └── README.md                # 完整实验教程
```

## 环境要求

- GitHub 账号
- DeepSeek API Key，且账号具有可用余额
- GitHub CLI `gh`
- gh-aw 扩展
- Python 3.10+

安装并检查 gh-aw：

```bash
gh extension install github/gh-aw
gh aw --version
```

## 配置 DeepSeek API Key

在 GitHub 仓库的 **Settings → Secrets and variables → Actions** 中添加 Repository Secret：

```text
Name:  DEEPSEEK_API_KEY
Value: 你的 DeepSeek API Key
```

也可以通过 GitHub CLI 设置：

```bash
gh secret set DEEPSEEK_API_KEY
```

不要将真实 API Key 写入代码、`.env.example` 或任何 Git 提交。

## 编译和运行工作流

在仓库根目录执行：

```bash
gh aw compile .github/workflows/tech-insight.md
gh workflow run "EV Insight Workflow"
```

也可以进入 GitHub 仓库的 **Actions** 页面，选择 **EV Insight Workflow** 后手动运行。

工作流完成后会创建包含最新报告的 Pull Request。主要输出包括：

- `Lab-01-Tech-Insights/output/raw_signals.json`
- `Lab-01-Tech-Insights/output/clusters/hotspots.json`
- `Lab-01-Tech-Insights/output/insights/insights.json`
- `Lab-01-Tech-Insights/output/report.md`
- `Lab-01-Tech-Insights/frontend/report.md`

## 本地诊断

本地脚本不调用 DeepSeek，而是使用确定性 fallback 验证 Python 工具链：

```bash
python Lab-01-Tech-Insights/run_local_pipeline.py
```

预览前端报告：

```bash
python -m http.server 8000 --directory Lab-01-Tech-Insights/frontend
```

然后访问 `http://localhost:8000`。

## 更多说明

完整实验步骤、工作流阶段与故障排查请参阅 [Lab-01-Tech-Insights/README.md](Lab-01-Tech-Insights/README.md)。
