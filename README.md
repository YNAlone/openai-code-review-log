# openai-code-review-log
<div align="center"><h1>Code Guard 代码审查Agent</h1><p>基于Agentic Coding理念的企业级自动化代码审查工具</p><p><img src="https://img.shields.io/badge/Java-8-blue.svg" alt="Java"><img src="https://img.shields.io/badge/Spring%20Boot-2.7-green.svg" alt="Spring Boot"><img src="https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-orange.svg" alt="GitHub Actions"><img src="https://img.shields.io/badge/ChatGLM-4-green.svg" alt="ChatGLM"></p></div>
项目简介
Code Guard 是一个面向研发全流程的 AI 代码审查 Agent，采用多智能体协同架构，深度嵌入 GitHub Actions CI/CD 流水线，实现代码提交→智能诊断→多维度评审→报告归档→实时通知的全流程自动化闭环。
针对传统人工 Code Review 时效性差、标准不统一、易遗漏问题的痛点，Code Guard 能够在 15 秒内完成一次完整的代码审查，覆盖代码性能、安全隐患、逻辑缺陷、规范合规等 8 个核心维度，大幅降低团队代码审查成本。
✨ 核心特性
🤖 多智能体协同架构：拆分协调、感知、认知、执行、通知 5 个职责清晰的专项智能体，低耦合高内聚
⚡ CI/CD 深度集成：原生适配 GitHub Actions，仅需 100 行 YAML 配置即可完成接入，零代码侵入
📊 多维度代码评审：覆盖代码性能、安全隐患、逻辑缺陷、规范合规等 8 个核心评审维度
🔔 实时通知：支持微信模板消息推送，代码审查完成后第一时间通知开发者
📝 自动报告归档：评审报告自动归档到专属 GitHub 仓库，永久留存可追溯
🚀 极致性能：单轮评审平均耗时仅 15 秒，支持高频次代码提交场景
🚀 快速开始
1. Fork 本仓库
点击右上角的 Fork 按钮，将本仓库复制到你的 GitHub 账号下。
2. 配置 GitHub Secrets
进入仓库的Settings → Secrets and variables → Actions页面，添加以下 10 个 Secret：
表格
Secret 名称	对应的值	获取地址
CODE_REVIEW_LOG_URI	https://github.com/你的用户名/openai-code-review-log	新建一个日志仓库
CODE_TOKEN	GitHub 个人访问令牌（PAT）	https://github.com/settings/tokens
WEIXIN_APPID	微信测试号 appID	https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo
WEIXIN_SECRET	微信测试号 appsecret	同上
WEIXIN_TOUSER	接收通知的微信号	同上
WEIXIN_TEMPLATE_ID	微信模板消息 ID	同上
CHATGLM_APIHOST	https://open.bigmodel.cn/api/paas/v4/chat/completions	智谱 AI 官方地址
CHATGLM_APIKEYSECRET	智谱 AI API Key	https://open.bigmodel.cn/usercenter/apikeys
3. 触发代码审查
提交任意代码到 master 分支，GitHub Actions 会自动触发代码审查，完成后你会收到微信通知。
📊 测试数据与稳定性
为了验证系统的稳定性和性能，我进行了连续 100 次 CI/CD 批量测试：
✅ 成功率：100%（100 次执行全部成功，无中断）
⏱️ 平均执行耗时：15 秒
🎯 代码问题识别覆盖率：100%
🔄 支持并发数：10 个并行任务
测试方法：基于 GitHub Actions 批量执行能力，模拟真实开发者提交代码场景，连续触发 100 次代码审查。
🏗️ 项目架构
plaintext
Code Guard
├── 协调智能体（Coordinator Agent）：负责编排整个执行流程
├── 感知智能体（Perception Agent）：提取Git Diff代码变更
├── 认知智能体（Cognition Agent）：调用大模型进行代码评审
├── 执行智能体（Execution Agent）：生成并归档评审报告
└── 通知智能体（Notification Agent）：发送微信通知
🛠️ 技术栈
后端框架：Java 8 + Spring Boot
大模型：智谱 AI ChatGLM 4
代码操作：JGit
CI/CD：GitHub Actions
通知：微信公众平台 API
缓存：Guava Cache
构建工具：Maven
📸 运行截图
GitHub Actions 运行效果


微信通知效果


评审报告示例
plaintext
## 代码审查报告
**项目**：openai-code-review
**分支**：master
**提交人**：YNAlone
**提交信息**：feat: 添加异常处理机制

### 代码评分：85分
### 问题列表
1. **异常处理缺失**：第45行未捕获IOException，可能导致程序崩溃
   - 修改建议：添加try-catch块捕获异常并记录日志

2. **命名不规范**：第78行变量名`a`无意义
   - 修改建议：改为`userCount`
🧪 测试用例
项目包含 24 个覆盖 8 大类常见代码问题的测试用例：
空指针异常类
SQL 注入风险类
命名不规范类
异常处理缺失类
资源未关闭类
低效代码类
安全隐患类
代码规范类
📈 性能优化
Guava Cache 缓存：实现鉴权 Token 本地复用，减少 90% 无效网络请求
指数退避重试：对网络临时性失败进行自动重试，提升系统稳定性
全链路异常处理：每个环节都有异常兜底，不会导致 CI/CD 流水线崩溃
资源自动清理：自动删除临时文件，避免磁盘泄漏
📄 许可证
本项目采用 MIT 许可证，详情请见LICENSE文件。
📞 联系我
GitHub：@YNAlone
邮箱：18690469919@163.com
