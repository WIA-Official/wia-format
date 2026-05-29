# `.wia` — The AI-Native Document Format

> **Humans write. AI executes. Machines verify. Robots converge.**

`.wia` is a Markdown superset. Every `.md` is a valid `.wia`.
What Markdown can't do, `.wia` adds — and nothing more.

```
Markdown  = read
.wia      = read + execute + verify + AI + Physical AI + IoT
```

---

## The Format Everyone Has Been Waiting For

No existing format combines all five:

| | Human-readable | Executable | AI-native | Self-verifying | Physical AI |
|---|---|---|---|---|---|
| Markdown | ✅ | ❌ | ❌ | ❌ | ❌ |
| Jupyter | ❌ (JSON) | ✅ | ❌ | ❌ | ❌ |
| AGENTS.md | ✅ | ❌ | ✅ | ❌ | ❌ |
| Terraform | ❌ | ✅ | ❌ | △ | ❌ |
| Ansible | ❌ (YAML) | ✅ | △ | ❌ | ❌ |
| RUNME | ✅ | ✅ | ❌ | ❌ | ❌ |
| **`.wia`** | **✅** | **✅** | **✅** | **✅** | **✅** |

---

## 45+ Formats Convert to .wia

`.wia` is the **superset** — everything below can come up:

**Documents & Config**: `.md` · `.txt` · `.rst` · `.adoc` · `.json` · `.yml` · `.toml` · `.ini` · `.xml` · `.env` · `.properties` · `.plist` · `.csv` · `.log`

**Programming**: `.sh` · `.py` · `.sql` · `.js` · `.ts` · `.go` · `.rs` · `.rb` · `.java` · `.c` · `.cpp` · `.lua` · `.ps1`

**Infrastructure**: `.tf` · `.hcl` · `Dockerfile` · `docker-compose.yml` · `Jenkinsfile` · `.gradle` · `Vagrantfile` · `Makefile` · `crontab` · `nginx.conf`

**API & Schema**: `.proto` · `.graphql` · `.prisma`

**Data Science**: `.ipynb` (Jupyter → .wia block conversion)

**Accessibility**: `.brf` · `.brl` (Braille)

---

## Features

### Block Types
`sh run` · `sql run on=` · `ai [model=]` · `verify expect=` · `python run` · `node run` · `display`

### Block Attributes
`run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` · `pipe` · `retry=` · `converge=` · `drift=`

### Input Types
`string` · `number` · `boolean` · `enum` · `secret` · `file` · `array`

### Special Variables
`{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` · `{{$os}}` · `{{$arch}}`

### Safety
Approval gates · Dry-run mode · Rollback (`on_fail=`) · Idempotency · Secret masking · Shell injection prevention

### AI Integration
Soomy auto-agent · Model selection · Vision images · AI analysis of results · AI .wia generation ("make me a runbook")

### Compliance
Execution log (audit trail) · HTML report export · SOC 2 / ISO 27001 / ISO 9001 evidence generation (21 controls)

### OS File Association (v3.9.0+)
Double-click `.wia` → WIA SOOM opens automatically (Windows/macOS/Linux)

### 10 Natural Creation Features (v3.9.0+)
1. Terminal gold banner (3+ commands → "Save as .wia?")
2. Always-visible W button for quick save
3. Soomy AI generates .wia on request
4. Session recording → .wia conversion
5. SFTP right-click "New .wia Runbook"
6. Ctrl+Shift+W quick create
7. 21-template gallery (6 categories)
8. Execution history dashboard
9. Monaco diff/merge for versions
10. `@include` transclusion

---

## Physical AI, ROS 2 & IoT

`.wia` is built for **robot fleet operations** and **IoT device management**:

### ROS 2 Robot Management
- SSH-based ROS 2 CLI bridge (18 IPC endpoints)
- Robot health monitoring (nodes, topics, services, battery, CPU temp)
- AI-powered robot diagnosis
- ros2 bag recording/playback/analysis
- Desired-state convergence engine
- Config drift detection (fleet-wide)
- Auto-generated .wia recovery runbooks

### IoT Device Management
Any device running Linux with SSH = .wia ready:
- 🍓 Raspberry Pi · 🏭 Smart factory sensors · 🌾 Smart farm
- 📹 CCTV/NVR · 🛜 Network equipment · 🚁 Drones · 🚗 Autonomous vehicles

### SW vs HW
`.wia` solves **software problems** (70-80% of all "failures"):
- Process crashes → restart ✅
- Memory issues → cleanup ✅
- Config errors → restore ✅
- Network drops → reconnect ✅
- **All remotely — no on-site visit needed**

Hardware failures (motor, sensor damage) require human hands, but `.wia` helps with diagnosis, prevention, and post-repair verification.

---

## 111 Example Runbooks

The [`examples/`](examples/) directory contains **111 production-ready runbooks** across 13 categories:

| Category | Count | Examples |
|----------|-------|---------|
| 🖥️ Server Setup | 7 | `amazon-linux-setup.wia`, `ubuntu-server-setup.wia`, `ssh-hardening.wia` |
| 🌐 Web Server | 8 | `wordpress-install.wia`, `nginx-install.wia`, `nodejs-deploy.wia` |
| 🗄️ Database | 7 | `mysql-install.wia`, `postgresql-backup.wia`, `redis-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`, `docker-compose-deploy.wia` |
| ☸️ Kubernetes | 5 | `k8s-cluster-check.wia`, `k8s-deploy-app.wia`, `helm-install-app.wia` |
| 📊 Monitoring | 5 | `prometheus-install.wia`, `disk-alert.wia`, `log-rotation.wia` |
| 🔒 Security | 7 | `security-audit.wia`, `fail2ban-setup.wia`, `ssl-cert-renewal.wia` |
| 🔄 CI/CD | 5 | `github-actions-setup.wia`, `terraform-apply.wia` |
| ☁️ Cloud | 5 | `aws-cli-setup.wia`, `s3-backup.wia`, `ec2-snapshot.wia` |
| 📧 Communication | 3 | `postfix-setup.wia`, `slack-webhook.wia` |
| 🤖 Robot/ROS | 9 | `ros-diagnostic.wia`, `ros-node-recovery.wia`, `ros2-install.wia` |
| 📱 Application | 4 | `pm2-deploy.wia`, `systemd-service.wia`, `crontab-setup.wia` |
| 🏥 Incident | 7 | `high-cpu-response.wia`, `disk-full-response.wia`, `oom-response.wia` |

---

## Ecosystem

| Tool | Role | Status |
|------|------|--------|
| **[WIA SOOM](https://wiasoom.com)** | Reference runtime (Win/Mac/Linux) | ✅ v3.9.1 |
| **[Spec v1](SPEC-v1.md)** | Formal specification (19 sections) | ✅ Published |
| **[111 Runbooks](examples/)** | Production-ready templates | ✅ Available |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | Format landing page | ✅ Live |
| **[Easy Guide](https://wia.wiasoom.com/easy-guide.html)** | Beginner-friendly guide | ✅ Live |
| **[Converter](https://wia.wiasoom.com/convert.html)** | 45+ formats → .wia | ✅ Live |
| **[Viewer](https://wia.wiasoom.com/view.html)** | Read .wia without install | ✅ Live |
| **[Training](https://rise.smilestory.ai/course/wia-format-robot-ops)** | 15-chapter course | ✅ Available |
| **Plugin Marketplace** | Runbook packs (FREE + PRO) | ✅ v3.9.0 |
| **Compliance Reports** | SOC2 + ISO27001 + ISO9001 | ✅ v3.8.5 |
| **Rust CLI** (`wia`) | Single binary converter/runner | 🔜 Roadmap |
| **VS Code Extension** | Syntax highlighting + preview | 🔜 Roadmap |

### Rust Tooling Roadmap

```
libwia (Rust core library)
├── wia CLI      → single binary converter/runner
├── WASM module  → browser tools at native speed (8-10x JS)
└── napi-rs      → Electron app integration
```

---

## Design Principles

1. **Markdown superset** — every `.md` is a valid `.wia`
2. **Human-first** — readable without any tool
3. **No auto-execution** — user must click Run (security)
4. **Language-agnostic** — 254 human languages, any programming language
5. **Portable** — plain text, no vendor lock-in
6. **Self-verifying** — built-in assertions
7. **AI-native** — AI can read, execute, extend, and verify
8. **Physical AI ready** — ROS 2 fleet operations + IoT
9. **Accessible** — WCAG AA, RTL, Braille, keyboard navigation

## MIME Type

`text/vnd.wia`

## License

Specification: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · Examples: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

Created by **[Smilestory Co., Ltd.](https://smilestory.net)** (WIA Standards) · [wiasoom.com](https://wiasoom.com)
