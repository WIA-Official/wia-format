# `.wia` — The AI-Native Document Format

> **Humans write. AI executes. Machines verify. Robots converge.**

`.wia` is a Markdown superset. Every `.md` is a valid `.wia`.
What Markdown can't do, `.wia` adds — and nothing more.

```
Markdown  = read
.wia      = read + execute + verify + AI + Physical AI
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

## 22 Features

| Category | Features |
|----------|----------|
| **Block Types** | `sh run` · `sql run on=` · `ai` · `verify expect=` · `python run` · `node run` |
| **Attributes** | `run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` |
| **Inputs** | `string` · `number` · `boolean` · `enum` · `secret` · `file` · `array` |
| **Variables** | `{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` |
| **Safety** | Approval gates · Dry-run · Rollback · Idempotency · Secret masking |
| **AI** | Soomy agent · Model selection · Vision images · Auto-analysis |
| **Compliance** | Execution log · HTML export · SOC 2 / ISO 27001 evidence |

---

## Physical AI & ROS 2

`.wia` is built for **robot fleet operations**:

```yaml
---
wia: "1"
title: Robot Fleet Health Check
agent: soomy
---
```

````markdown
```sh run
ros2 node list
```

```verify expect=0
ros2 node info /navigation_node
```

```ai model=gpt-4o
Analyze robot health and recommend maintenance.
```
````

**The gap .wia fills**: NVIDIA builds the brain (GR00T), FANUC/ABB build the body — but **no standard tool manages deployed robot fleets**. `.wia` is that missing operations layer.

---

## Ecosystem

| Tool | Role | Status |
|------|------|--------|
| **[WIA SOOM](https://wiasoom.com)** | Reference runtime (Win/Mac/Linux) | ✅ v3.8.5 |
| **[Spec v1](SPEC-v1.md)** | Formal specification (19 sections) | ✅ Published |
| **[12 Example Runbooks](examples/)** | Production-ready templates | ✅ Available |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | Format landing page | ✅ Live |
| **[Training Course](https://rise.smilestory.ai/course/wia-format-robot-ops)** | 15-chapter hands-on | ✅ Available |
| **Web Converter** | 45+ formats → .wia (browser-side) | 🔜 Coming soon |
| **Web Viewer** | Read .wia without install | 🔜 Coming soon |
| **Rust CLI** (`wia`) | Single binary, no runtime | 🔜 Roadmap |
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
8. **Physical AI ready** — ROS 2 fleet operations
9. **Accessible** — WCAG AA, RTL, Braille, keyboard navigation

## MIME Type

`text/vnd.wia`

## License

Specification: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · Examples: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

Created by **[Smilestory Co., Ltd.](https://smilestory.net)** (WIA Standards) · [wiasoom.com](https://wiasoom.com)
