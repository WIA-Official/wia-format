# `.wia` — AI 原生文档格式

**语言:** [English](README.md) · [한국어](README.ko.md) · 中文 · [日本語](README.ja.md) · [Español](README.es.md) · [العربية](README.ar.md)

> **人类编写，AI 执行，机器验证,机器人收敛。**

`.wia` 是 Markdown 的超集。每个 `.md` 都是合法的 `.wia`。
Markdown 做不到的，`.wia` 来补足 —— 不多也不少。

```
Markdown  = 阅读
.wia      = 阅读 + 执行 + 验证 + AI + 物理 AI + IoT
```

---

## 大家期待已久的格式

没有任何现有格式同时具备这五项：

|            | 人类可读 | 可执行 | AI 原生 | 自验证 | 物理 AI |
| ---------- | -------- | ------ | ------- | ------ | ------- |
| Markdown   | ✅        | ❌      | ❌       | ❌      | ❌       |
| Jupyter    | ❌ (JSON) | ✅      | ❌       | ❌      | ❌       |
| AGENTS.md  | ✅        | ❌      | ✅       | ❌      | ❌       |
| Terraform  | ❌        | ✅      | ❌       | △      | ❌       |
| Ansible    | ❌ (YAML) | ✅      | △       | ❌      | ❌       |
| RUNME      | ✅        | ✅      | ❌       | ❌      | ❌       |
| **`.wia`** | **✅**    | **✅**  | **✅**   | **✅**  | **✅**   |

---

## 45+ 种格式可转换为 .wia

`.wia` 是**超集** —— 以下所有格式都可以向上转换：

**文档与配置**：`.md` · `.txt` · `.rst` · `.adoc` · `.json` · `.yml` · `.toml` · `.ini` · `.xml` · `.env` · `.properties` · `.plist` · `.csv` · `.log`

**编程**：`.sh` · `.py` · `.sql` · `.js` · `.ts` · `.go` · `.rs` · `.rb` · `.java` · `.c` · `.cpp` · `.lua` · `.ps1`

**基础设施**：`.tf` · `.hcl` · `Dockerfile` · `docker-compose.yml` · `Jenkinsfile` · `.gradle` · `Vagrantfile` · `Makefile` · `crontab` · `nginx.conf`

**API 与 Schema**：`.proto` · `.graphql` · `.prisma`

**数据科学**：`.ipynb`（Jupyter → .wia 块转换）

**无障碍**：`.brf` · `.brl`（盲文）

---

## 功能

### 块类型
`sh run` · `sql run on=` · `ai [model=]` · `verify expect=` · `python run` · `node run` · `display`

### 块属性
`run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` · `pipe` · `retry=` · `converge=` · `drift=`

### 输入类型
`string` · `number` · `boolean` · `enum` · `secret` · `file` · `array`

### 特殊变量
`{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` · `{{$os}}` · `{{$arch}}`

### 安全性
审批门控 · 试运行模式 · 回滚（`on_fail=`）· 幂等性 · 密钥脱敏 · Shell 注入防护

### AI 集成
Soomy 自动代理 · 模型选择 · 视觉图像 · 结果 AI 分析 · AI 生成 .wia（“帮我做个 runbook”）

### 合规
执行日志（审计追踪）· HTML 报告导出 · SOC 2 / ISO 27001 / ISO 9001 证据生成（**22 项自动化控制** —— SOC 2 9 项、ISO 27001 8 项、ISO 9001 5 项）

---

## 可用 254 种语言中任意一种编写

`.wia` 是纯 UTF-8 文本。作者用自己的语言书写 —— 无论散文使用何种人类语言，运行时都以相同方式执行。

这并非空谈，而是体现在示例中。例如 [`examples/server-health.wia`](examples/server-health.wia) 以韩语编写（`title: WIA SOOM 서버 건강 점검`），运行方式与英文 runbook 完全一致。**254 种语言**中任意一种的现场操作员，都能用母语阅读、编写并运行 `.wia`，而 **WIA SOOM** 运行时界面也已本地化为全部 254 种语言。

无障碍同样秉持这一精神：WCAG AA、RTL 文字、盲文（`.brf` / `.brl`）以及完整的键盘导航。目标是打造一种运维格式 —— 法院、审计员、机器人，以及用母语工作的视障操作员都能读懂。

---

## 物理 AI、ROS 2 与 IoT

`.wia` 专为**机器人集群运维**与 **IoT 设备管理**而构建：

### ROS 2 机器人管理
- 基于 SSH 的 ROS 2 CLI 桥接（**27 个 IPC 端点**）
- 机器人健康监控（节点、话题、服务、电池、CPU 温度）
- AI 驱动的机器人诊断
- ros2 bag 录制 / 回放 / 分析
- 期望状态收敛引擎 + 配置漂移检测（集群范围）
- 自动生成 `.wia` 恢复 runbook

### IoT 设备管理
任何运行 Linux 并支持 SSH 的设备皆可用 `.wia`：树莓派 · 智能工厂传感器 · 智慧农场 · CCTV/NVR · 网络设备 · 无人机 · 自动驾驶车辆。

### 软件 vs 硬件
`.wia` 远程解决占运维“故障”大多数的**软件问题** —— 进程崩溃（重启）、内存问题（清理）、配置错误（恢复）、网络中断（重连）—— 无需现场出动。硬件故障（电机、传感器损坏）需人工处理，但 `.wia` 仍能协助诊断、预防和修复后验证。

---

## 111 个示例 Runbook

[`examples/`](examples) 目录包含 **111 个生产级 runbook**（已核实数量），覆盖 13 个类别：

| 类别 | 数量 | 示例 |
| ---- | ---- | ---- |
| 🖥️ 服务器 / OS | 13 | `amazon-linux-setup.wia`、`ssh-hardening.wia`、`linux-performance-tuning.wia` |
| 🌐 Web / 应用 | 10 | `nginx-install.wia`、`wordpress-install.wia`、`nodejs-deploy.wia`、`pm2-deploy.wia` |
| 🗄️ 数据库 | 10 | `mysql-install.wia`、`postgresql-backup.wia`、`redis-install.wia`、`mongodb-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`、`docker-compose-deploy.wia`、`docker-registry.wia` |
| ☸️ Kubernetes | 9 | `k8s-cluster-check.wia`、`k8s-rollback.wia`、`helm-install-app.wia` |
| 📊 监控 / 日志 | 9 | `prometheus-install.wia`、`elk-stack-setup.wia`、`log-investigation.wia` |
| 🔒 安全 / 合规 | 13 | `security-audit.wia`、`fail2ban-setup.wia`、`ssl-cert-renewal.wia`、`aws-iam-audit.wia` |
| 🔄 CI/CD / IaC | 6 | `github-actions-setup.wia`、`terraform-apply.wia`、`ansible-playbook-run.wia` |
| ☁️ 云 / AWS | 8 | `aws-cli-setup.wia`、`s3-backup.wia`、`ec2-snapshot.wia`、`autoscaling-setup.wia` |
| 🌍 网络 / DNS | 6 | `network-troubleshoot.wia`、`dns-troubleshoot.wia`、`site-failover-dns.wia` |
| 📧 通信 | 3 | `postfix-setup.wia`、`smtp-test.wia`、`slack-webhook.wia` |
| 🤖 机器人 / ROS 2 | 10 | `ros-diagnostic.wia`、`ros-node-recovery.wia`、`robot-fleet-health.wia`、`ros2-bag-record.wia` |
| 🏥 事故 / DR | 10 | `high-cpu-response.wia`、`oom-response.wia`、`disk-full-response.wia`、`disaster-recovery-plan.wia` |

---

## 生态系统

| 工具 | 角色 | 状态 |
| ---- | ---- | ---- |
| **[WIA SOOM](https://wiasoom.com)** | 参考运行时（Win/Mac/Linux） | ✅ v3.9.29 |
| **[Spec v1](SPEC-v1.md)** | 正式规范（19 个章节） | ✅ 已发布 |
| **[111 个 Runbook](examples)** | 生产级模板 | ✅ 可用 |
| **[论文 (Zenodo)](https://doi.org/10.5281/zenodo.20448006)** | 可引用预印本 + DOI (CC-BY 4.0) | ✅ 已发布 |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | 格式主页 | ✅ 在线 |
| **[转换器](https://wia.wiasoom.com/convert.html)** | 45+ 种格式 → .wia | ✅ 在线 |
| **[查看器](https://wia.wiasoom.com/view.html)** | 无需安装即可阅读 .wia | ✅ 在线 |
| **Rust CLI** (`wia`) | 单一二进制转换/执行器 | 🔜 路线图 |
| **VS Code 扩展** | 语法高亮 + 预览 | 🔜 路线图 |

### Rust 工具链路线图

```
libwia (Rust 核心库)
├── wia CLI      → 单一二进制转换/执行器
├── WASM 模块    → 以原生速度运行的浏览器工具
└── napi-rs      → Electron 应用集成
```

---

## 设计原则

1. **Markdown 超集** —— 每个 `.md` 都是合法的 `.wia`
2. **以人为先** —— 无需任何工具即可阅读
3. **禁止自动执行** —— 用户须点击 Run（安全）
4. **语言无关** —— 254 种人类语言，任意编程语言
5. **可移植** —— 纯文本，无供应商锁定
6. **自验证** —— 内置断言
7. **AI 原生** —— AI 可阅读、执行、扩展和验证
8. **物理 AI 就绪** —— ROS 2 集群运维 + IoT
9. **无障碍** —— WCAG AA、RTL、盲文、键盘导航

## 引用

若在学术或技术工作中引用 `.wia`，请引用该预印本：

> Yeon, Sam-heum. *.wia: An AI-Native Document Format for Executable, Self-Verifying Operations in Physical AI.* Zenodo, 2026. https://doi.org/10.5281/zenodo.20448006

## MIME 类型

`text/vnd.wia`

## 许可证

规范：[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · 示例：[Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

由 **[Smilestory Co., Ltd.](https://smilestory.net)**（WIA Standards）创建 · [wiasoom.com](https://wiasoom.com)
