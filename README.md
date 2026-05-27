# `.wia` — AI-Native Document Format

> **The file format where humans write, AI executes, and machines verify.**

`.wia` is a Markdown superset. Every `.md` is a valid `.wia`.
What Markdown can't do, `.wia` adds — and nothing more.

```
Markdown  = read
.wia      = read + execute + verify + AI
```

## What is .wia?

`.wia` adds four things to Markdown:

1. **Typed metadata** — YAML front-matter with version, agent, typed inputs
2. **Executable blocks** — `sh run`, `sql run on=db`, `ai`, `verify expect=0`
3. **Multimodal** — `{ai:vision}` images, AI-readable embeds
4. **Source + Verification** — `> src: URL` attribution, self-verifying assertions

Everything else is standard Markdown. No new syntax to learn.

## Quick Example

```yaml
---
wia: "1"
title: Server Health Check
agent: soomy
inputs:
  server: { type: string, default: "prod-1" }
---
```

````markdown
# Server Health Check

## Check disk usage

```sh run
df -h /
```

## Verify service is running

```verify expect=0
systemctl is-active nginx
```

## AI analysis

```ai
Analyze the output above and suggest optimizations.
```
````

## Why .wia?

| Problem | Before | With .wia |
|---------|--------|-----------|
| 3 AM incident | Copy commands from wiki → mistakes | **Run All → auto-recovery + PASS/FAIL** |
| New engineer onboarding | "Read this doc" → 2 weeks | **.wia tutorial → 1 day** |
| SOC 2 audit evidence | Manual screenshots | **Execution log = automatic evidence** |
| Robot fleet recovery | SSH → manual ros2 commands | **.wia runbook → auto-diagnose + recover** |

## The Gap .wia Fills

No existing format combines all four:

| | Human-readable | Executable | AI-native | Self-verifying |
|---|---|---|---|---|
| Markdown | ✅ | ❌ | ❌ | ❌ |
| Jupyter | ❌ (JSON) | ✅ | ❌ | ❌ |
| AGENTS.md | ✅ | ❌ | ✅ | ❌ |
| Terraform | ❌ | ✅ | ❌ | △ |
| Ansible | ❌ (YAML) | ✅ | △ | ❌ |
| **`.wia`** | **✅** | **✅** | **✅** | **✅** |

## Specification

See [SPEC-v1.md](SPEC-v1.md) — the complete v1 specification (19 sections, RFC 2119 language).

## Examples

The [`examples/`](examples/) directory contains 12 production-ready runbooks:

| File | Category | Description |
|------|----------|-------------|
| `ros-diagnostic.wia` | 🤖 Robot | ROS 2 full robot health check |
| `ros-node-recovery.wia` | 🤖 Robot | ROS node failure recovery with rollback |
| `ros-sensor-check.wia` | 🤖 Robot | Sensor topic frequency + data quality |
| `robot-fleet-health.wia` | 🤖 Robot | Multi-robot fleet health inspection |
| `server-health.wia` | 🖥️ Server | Server disk/memory/service check |
| `server-incident-response.wia` | 🖥️ Server | Incident response SOP with AI analysis |
| `incident-response.wia` | 🖥️ Server | PM2 service recovery runbook |
| `database-maintenance.wia` | 🖥️ Server | Database health + maintenance |
| `fleet-rollout.wia` | 🌐 Fleet | Software deployment across fleet |
| `kubernetes-pod-recovery.wia` | 🌐 Fleet | K8s pod recovery + monitoring |
| `ssl-cert-renewal.wia` | 🔒 Security | SSL certificate check + renewal |
| `security-audit.wia` | 🔒 Security | CIS benchmark security audit |

## Reference Runtime

**[WIA SOOM](https://wiasoom.com)** is the reference runtime for `.wia` files.

- Open any `.wia` file → WiaDocRunner renders it with Run buttons
- Execute blocks with one click (Run) or all at once (Run All)
- Built-in AI integration (Soomy agent analyzes execution results)
- 254 language support
- Export to HTML report (compliance evidence)
- Robot fleet management with .wia runbook execution

## Design Principles

1. **Markdown superset** — every `.md` is a valid `.wia`
2. **Human-first** — readable without any tool
3. **No auto-execution** — user must click Run (security)
4. **Language-agnostic** — 254 human languages, any programming language
5. **Portable** — plain text, no vendor lock-in
6. **Self-verifying** — built-in assertions
7. **AI-native** — AI can read, execute, extend, and verify

## MIME Type

`text/vnd.wia`

## License

Specification: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)
Examples: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

## Who

Created by **[SmileStory Inc.](https://wiasoom.com)** (WIA Standards)
Maintained at **[WIA-Official/wia-format](https://github.com/WIA-Official/wia-format)**

---

*`.wia` is an open standard. The spec is public. The reference runtime is [WIA SOOM](https://wiasoom.com) — free to download.*
