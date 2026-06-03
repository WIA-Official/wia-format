# `.wia` — The AI-Native Document Format

**Read in:** English · [한국어](README.ko.md) · [中文](README.zh.md) · [日本語](README.ja.md) · [Español](README.es.md) · [العربية](README.ar.md)

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

|            | Human-readable | Executable | AI-native | Self-verifying | Physical AI |
| ---------- | -------------- | ---------- | --------- | -------------- | ----------- |
| Markdown   | ✅              | ❌          | ❌         | ❌              | ❌           |
| Jupyter    | ❌ (JSON)       | ✅          | ❌         | ❌              | ❌           |
| AGENTS.md  | ✅              | ❌          | ✅         | ❌              | ❌           |
| Terraform  | ❌              | ✅          | ❌         | △              | ❌           |
| Ansible    | ❌ (YAML)       | ✅          | △         | ❌              | ❌           |
| RUNME      | ✅              | ✅          | ❌         | ❌              | ❌           |
| **`.wia`** | **✅**          | **✅**      | **✅**     | **✅**          | **✅**       |

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
Execution log (audit trail) · HTML report export · SOC 2 / ISO 27001 / ISO 9001 evidence generation (**22 automated controls** — 9 SOC 2, 8 ISO 27001, 5 ISO 9001)

---

## Written in Any of 254 Languages

A `.wia` is plain UTF-8 text. The author writes in their own language — the runtime executes identically regardless of the human language of the prose.

This is not a claim; it is in the examples. For instance, [`examples/server-health.wia`](examples/server-health.wia) is authored in Korean (`title: WIA SOOM 서버 건강 점검`) and runs exactly like an English runbook. A field operator in any of **254 languages** can read, write, and run `.wia` in their mother tongue, and the **WIA SOOM** runtime UI is localized to all 254.

Accessibility is built in the same spirit: WCAG AA, RTL scripts, Braille (`.brf` / `.brl`), and full keyboard navigation. The goal is one operational format that a court, an auditor, a robot, and a blind operator in their native language can all read.

---

## Physical AI, ROS 2 & IoT

`.wia` is built for **robot fleet operations** and **IoT device management**:

### ROS 2 Robot Management
- SSH-based ROS 2 CLI bridge (**27 IPC endpoints**)
- Robot health monitoring (nodes, topics, services, battery, CPU temp)
- AI-powered robot diagnosis
- ros2 bag recording / playback / analysis
- Desired-state convergence engine + config drift detection (fleet-wide)
- Auto-generated `.wia` recovery runbooks

### IoT Device Management
Any device running Linux with SSH = `.wia` ready: Raspberry Pi · smart-factory sensors · smart farm · CCTV/NVR · network equipment · drones · autonomous vehicles.

### Software vs Hardware
`.wia` resolves **software problems** (the majority of operational "failures") remotely — process crashes (restart), memory issues (cleanup), config errors (restore), network drops (reconnect) — with no on-site visit. Hardware failures (motor, sensor damage) need human hands, but `.wia` still helps with diagnosis, prevention, and post-repair verification.

---

## 111 Example Runbooks

The [`examples/`](examples) directory contains **111 production-ready runbooks** (verified count) across 13 categories:

| Category | Count | Examples |
| -------- | ----- | -------- |
| 🖥️ Server / OS | 13 | `amazon-linux-setup.wia`, `ssh-hardening.wia`, `linux-performance-tuning.wia` |
| 🌐 Web / App | 10 | `nginx-install.wia`, `wordpress-install.wia`, `nodejs-deploy.wia`, `pm2-deploy.wia` |
| 🗄️ Database | 10 | `mysql-install.wia`, `postgresql-backup.wia`, `redis-install.wia`, `mongodb-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`, `docker-compose-deploy.wia`, `docker-registry.wia` |
| ☸️ Kubernetes | 9 | `k8s-cluster-check.wia`, `k8s-rollback.wia`, `helm-install-app.wia` |
| 📊 Monitoring / Logging | 9 | `prometheus-install.wia`, `elk-stack-setup.wia`, `log-investigation.wia` |
| 🔒 Security / Compliance | 13 | `security-audit.wia`, `fail2ban-setup.wia`, `ssl-cert-renewal.wia`, `aws-iam-audit.wia` |
| 🔄 CI/CD / IaC | 6 | `github-actions-setup.wia`, `terraform-apply.wia`, `ansible-playbook-run.wia` |
| ☁️ Cloud / AWS | 8 | `aws-cli-setup.wia`, `s3-backup.wia`, `ec2-snapshot.wia`, `autoscaling-setup.wia` |
| 🌍 Network / DNS | 6 | `network-troubleshoot.wia`, `dns-troubleshoot.wia`, `site-failover-dns.wia` |
| 📧 Communication | 3 | `postfix-setup.wia`, `smtp-test.wia`, `slack-webhook.wia` |
| 🤖 Robot / ROS 2 | 10 | `ros-diagnostic.wia`, `ros-node-recovery.wia`, `robot-fleet-health.wia`, `ros2-bag-record.wia` |
| 🏥 Incident / DR | 10 | `high-cpu-response.wia`, `oom-response.wia`, `disk-full-response.wia`, `disaster-recovery-plan.wia` |

---

## Ecosystem

| Tool | Role | Status |
| ---- | ---- | ------ |
| **[WIA SOOM](https://wiasoom.com)** | Reference runtime (Win/Mac/Linux) | ✅ v3.9.29 |
| **[Spec v1](SPEC-v1.md)** | Formal specification (19 sections) | ✅ Published |
| **[111 Runbooks](examples)** | Production-ready templates | ✅ Available |
| **[Paper (Zenodo)](https://doi.org/10.5281/zenodo.20448006)** | Peer-citable preprint + DOI (CC-BY 4.0) | ✅ Published |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | Format landing page | ✅ Live |
| **[Converter](https://wia.wiasoom.com/convert.html)** | 45+ formats → .wia | ✅ Live |
| **[Viewer](https://wia.wiasoom.com/view.html)** | Read .wia without install | ✅ Live |
| **Rust CLI** (`wia`) | Single binary converter/runner | 🔜 Roadmap |
| **VS Code Extension** | Syntax highlighting + preview | 🔜 Roadmap |

### Rust Tooling Roadmap

```
libwia (Rust core library)
├── wia CLI      → single binary converter/runner
├── WASM module  → browser tools at native speed
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

## Citation

If you reference `.wia` in academic or technical work, please cite the preprint:

> Yeon, Sam-heum. *.wia: An AI-Native Document Format for Executable, Self-Verifying Operations in Physical AI.* Zenodo, 2026. https://doi.org/10.5281/zenodo.20448006

## MIME Type

`text/vnd.wia`

## License

Specification: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · Examples: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

Created by **[Smilestory Co., Ltd.](https://smilestory.net)** (WIA Standards) · [wiasoom.com](https://wiasoom.com)
