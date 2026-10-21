# JD 简历匹配助手

面向所有求职者的 DeepSeek + Streamlit JD 简历匹配工具。产品只用实时输入的简历原文与目标 JD 分析，输出岗位匹配度、差距、修改建议和优化后的完整简历；项目型经历按“项目背景 / 核心工作 / 项目成果”优化；不保存简历/JD。

## 运行

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
export DEEPSEEK_API_KEY='你的 DeepSeek API Key'
streamlit run app.py
```

也可复制 `.streamlit/secrets.toml.example` 为 `.streamlit/secrets.toml`，再填入密钥。该文件已被 Git 忽略；不要将真实 API Key 提交到 GitHub 仓库。

未设置 API Key 时，应用可完整体验上传、解析、核对与结果展示流程，但分析结果为不调用模型的本地安全预览。

## 实现范围

- PDF/DOCX 文字解析，10MB 限制，扫描版 PDF 拦截
- 简历和 JD 清洗、长度上限、原文人工核对
- DeepSeek OpenAI 兼容接口，低随机性、严格 JSON 输出
- 系统约束、输入边界与严格 JSON 输出
- 项目型经历按项目背景、核心工作、项目成果结构化优化

产品设计、风险矩阵、测试用例、内测脚本和迭代计划见 `docs/`。

## 策略更新

简历优化方法论统一维护在 `config/resume_strategies.json`。每个模块都有稳定 ID、名称与可执行规则，应用会在每次 JD 分析时读取并发送给模型。更新规则时修改该文件的 `version`、`updated_at` 和对应模块，再通过 GitHub Pull Request 发布；也可以先用仓库中的“简历优化策略更新”Issue 模板提交待评审策略。

## 长期部署

将仓库连接至 Streamlit Community Cloud，入口文件选择 `app.py`，依赖文件选择 `requirements.txt`，并在该服务的 Secrets 配置中添加 `DEEPSEEK_API_KEY`。不要把 API Key 写入 GitHub 仓库。
