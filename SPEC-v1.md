# `.wia` — AI-Native Document Format Specification v1.0

> The file format where humans write, AI executes, and machines verify.
> CommonMark superset. Every `.md` is a valid `.wia`.

---

## Abstract

`.wia` is an open, plain-text document format that extends CommonMark Markdown with four capabilities: **typed metadata**, **executable blocks**, **multimodal embedding**, and **built-in verification**. A `.wia` document is simultaneously human-readable documentation, machine-executable runbook, AI-native prompt surface, and compliance evidence trail. The format adds no new syntax where CommonMark already provides one; it occupies only the extension points that CommonMark leaves undefined. Any conforming Markdown renderer MUST display a `.wia` file as valid Markdown. Any conforming `.wia` runtime MUST additionally interpret the executable, multimodal, and verification extensions defined herein.

## Status

**Draft Specification — v1.0**

- Specification version: `1`
- Date: 2026-05-27
- Reference runtime: **WIA SOOM** v3.5.0+ (SmileStory Inc.)
- License: CC BY 4.0 (specification text); implementations are unrestricted
- Canonical URL: `https://wiasoom.com/spec/wia-v1`
- Previous version: v0 (draft, 2026)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

---

## 1. Introduction

### 1.1 Motivation

Modern technical work lives in documents—runbooks, tutorials, audit checklists, deployment guides, data pipelines. Yet today's document formats force a choice:

- **Markdown** is universal and human-readable, but inert. Code blocks are decoration.
- **Jupyter notebooks** are executable, but JSON-native, hard to diff, and language-locked to Python.
- **Quarto / R Markdown** serve data science but assume a compilation step and specific toolchains.
- **RUNME** adds execution to Markdown but lacks AI integration, verification, and multimodal support.
- **Org-mode** is powerful but Emacs-only, with no modern AI story.
- **AGENTS.md / llms.txt** provide AI context but cannot execute, verify, or embed media.

The gap: **no format unifies documentation, execution, AI interaction, multimodal content, and verification in a single plain-text file that remains valid Markdown.**

`.wia` fills this gap. A DevOps engineer writes a deployment runbook in Markdown. The same file executes shell commands, queries databases, asks AI to analyze logs, embeds screenshots for AI vision, and verifies each step—all without leaving the document. The execution log becomes compliance evidence. The file remains readable in any Markdown viewer, editable in any text editor, and diffable in any VCS.

### 1.2 Design Principles

1. **Markdown superset** — Every `.md` file is a valid `.wia` file. Zero migration cost.
2. **Human-first, machine-enhanced** — A `.wia` file MUST be readable and useful without any runtime. The runtime enhances, never gates.
3. **Explicit execution only** — No block SHALL execute on document open. Execution requires deliberate user action (security by design).
4. **Language-agnostic** — The format supports 254 human languages for content and any programming language for executable blocks.
5. **Portable** — Plain UTF-8 text. No binary blobs, no vendor lock-in, no proprietary encoding.
6. **Self-verifying** — Built-in assertion blocks produce PASS/FAIL evidence without external test frameworks.
7. **AI-native** — AI models can read, execute, extend, and verify `.wia` documents as first-class participants.

### 1.3 Terminology

- **Document** — A single `.wia` file.
- **Runtime** — Software that interprets `.wia` extensions (e.g., WIA SOOM).
- **Renderer** — Software that displays `.wia` as formatted text (any Markdown renderer qualifies).
- **Block** — A fenced code block (CommonMark) with optional `.wia` attributes.
- **Executable block** — A block with the `run` attribute or a recognized runner type (`ai`, `verify`).
- **Actor** — The entity that triggered execution: `human`, `ai`, or a specific model identifier.

---

## 2. Conformance

### 2.1 CommonMark Baseline

A conforming `.wia` runtime MUST pass **all** CommonMark 0.31.2 specification tests without modification. The `.wia` format SHALL NOT alter the parsing or rendering of any construct defined by CommonMark.

### 2.2 Extension Points

`.wia` extensions use ONLY the following mechanisms, all of which CommonMark leaves undefined or open:

1. **YAML front-matter** — The `---` delimited block before body content. CommonMark treats this as a thematic break followed by content; `.wia` interprets it as YAML metadata.
2. **Info-string attributes** — Additional tokens after the language identifier in fenced code block info strings (e.g., `` ```sh run ``). CommonMark specifies that the info string's first word is the language; subsequent words are unspecified.
3. **Curly-brace attributes on images** — `{ai:vision}` after image references. CommonMark does not define curly-brace attribute syntax; this follows the pattern established by Pandoc, Kramdown, and others.
4. **Blockquote conventions** — `> src: URL` lines. CommonMark defines blockquotes but not their semantic subtypes.

### 2.3 Conformance Levels

- **Level 0 (Renderer)** — Displays `.wia` as valid Markdown. Any CommonMark renderer achieves this.
- **Level 1 (Reader)** — Parses front-matter and recognizes executable blocks (displays them with visual indicators).
- **Level 2 (Runner)** — Executes blocks, resolves variables, records execution logs.
- **Level 3 (Full)** — All of the above plus AI block execution, multimodal processing, and verification.

---

## 3. Document Structure

A `.wia` document consists of two parts: an OPTIONAL front-matter header and a body.

```
+---------------------------+
| --- (YAML front-matter)   |  <- Optional
| ---                       |
+---------------------------+
| Body (CommonMark + ext)   |  <- Required
+---------------------------+
```

### 3.1 Front-matter (YAML)

If present, the front-matter MUST be the very first content in the file, delimited by two lines each containing exactly `---` (three hyphens). The content between delimiters MUST be valid YAML 1.2.

#### 3.1.1 Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `wia` | string | Format version. MUST be `"1"` for this specification. |

When the `wia` field is absent, the file MUST be treated as plain Markdown (Level 0 conformance). A runtime SHOULD still attempt to detect and honor executable blocks for user convenience but MUST NOT auto-execute them.

#### 3.1.2 Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Human-readable document title. |
| `lang` | string | Primary language of the document (BCP 47 tag, e.g., `en`, `ko`, `ar`). Defaults to `en`. |
| `agent` | string \| object | AI agent configuration. See S11. |
| `inputs` | object | Typed input parameters. See S5 and S7. |
| `outputs` | object | Declared output artifacts. |
| `tags` | array of strings | Classification tags (e.g., `[devops, deploy, staging]`). |
| `timeout` | integer | Default execution timeout in seconds for all blocks. Defaults to `30`. |
| `trust` | string | Trust level: `local`, `remote`, or `cloud`. See S10.4. Defaults to `local`. |
| `$schema` | string | URL of a JSON Schema for front-matter validation. |

#### 3.1.3 Example Front-matter

```yaml
---
wia: "1"
title: Production Health Check
lang: en
agent:
  role: SRE assistant
  rules:
    - Never execute DROP or DELETE without confirmation
    - Always explain before running destructive commands
  model: gpt-4o
inputs:
  environment:
    type: enum
    of: [staging, production]
    default: staging
    description: Target environment
  db_password:
    type: secret
    description: Database password (will not be logged)
outputs:
  report:
    type: file
    path: ./health-report-{{$timestamp}}.json
tags: [devops, health-check, production]
timeout: 60
trust: remote
---
```

### 3.2 Body

The body is standard CommonMark with the extensions defined in S4-S6. All CommonMark constructs (headings, lists, tables, links, emphasis, etc.) work exactly as specified by CommonMark 0.31.2.

---

## 4. Executable Blocks

Executable blocks are fenced code blocks whose info string contains a recognized runner keyword. A runtime MUST visually distinguish executable blocks from display-only code blocks (e.g., with a "Run" button, a colored border, or an icon).

### 4.1 Shell Blocks (`sh run`)

Execute a command in the system shell.

**Syntax:**

    ```sh run
    <shell commands>
    ```

**Behavior:**
- The runtime MUST execute the block content as a shell script via the user's default shell (or `/bin/sh` as fallback).
- Standard output and standard error MUST be captured and displayed inline below the block.
- The exit code MUST be recorded in the execution log (S9).
- If the exit code is non-zero, the runtime SHOULD visually indicate failure.

**Example:**

    ```sh run
    kubectl get pods -n production --no-headers | wc -l
    ```

### 4.2 SQL Blocks (`sql run`)

Execute a SQL query against a named database connection.

**Syntax:**

    ```sql run on=<connection-name>
    <SQL query>
    ```

**Behavior:**
- The `on` attribute MUST specify a connection identifier known to the runtime.
- The runtime MUST execute the query and display results as a Markdown table.
- The runtime MUST NOT execute DDL or DML statements (`CREATE`, `DROP`, `INSERT`, `UPDATE`, `DELETE`, `ALTER`, `TRUNCATE`) without explicit user confirmation.
- Query results SHOULD be limited to a configurable maximum row count (default: 1000).

**Example:**

    ```sql run on=clinic_db
    SELECT department, COUNT(*) as patient_count
    FROM patients
    WHERE admitted_date > CURRENT_DATE - INTERVAL '7 days'
    GROUP BY department
    ORDER BY patient_count DESC;
    ```

### 4.3 AI Blocks (`ai`)

Send a prompt to an AI model and insert the response into the document.

**Syntax:**

    ```ai [model=<model-id>]
    <prompt text>
    ```

**Behavior:**
- The runtime MUST send the block content as a prompt to the configured AI model.
- If `model` is specified, that model MUST be used. Otherwise, the runtime SHOULD use the model specified in front-matter `agent.model`, falling back to the runtime's default model.
- The AI response MUST be inserted below the block, clearly attributed as AI-generated.
- The runtime SHOULD pass relevant document context (front-matter, preceding blocks, execution results) as system context to the model.
- Variable substitution (S5) MUST be performed on the prompt before sending.

**Example:**

    ```ai model=claude-sonnet
    Analyze the following error log and provide:
    1. Root cause (one sentence)
    2. Severity (critical/high/medium/low)
    3. Recommended fix

    {{$prev}}
    ```

### 4.4 Verification Blocks (`verify`)

Execute a command and assert its output matches an expected value.

**Syntax:**

    ```verify expect=<expected-value>
    <shell command>
    ```

**Behavior:**
- The runtime MUST execute the command and compare its trimmed standard output against the `expect` value.
- If they match, the block is marked **PASS**. If they differ, **FAIL**.
- The result (PASS/FAIL), actual output, expected output, and timestamp MUST be recorded in the execution log.
- A `verify` block with `expect=0` SHOULD be interpreted as asserting exit code 0 (success) rather than output string "0", unless the output is explicitly "0".

**Example:**

    ```verify expect=active
    systemctl is-active nginx
    ```

### 4.5 Display Blocks (no `run` attribute)

A fenced code block without `run`, `ai`, or `verify` in its info string is a **display block**. It MUST be rendered exactly as CommonMark specifies—as a formatted code listing with optional syntax highlighting. A runtime MUST NOT execute display blocks.

**Example:**

    ```python
    # This is just documentation — it will NOT execute
    def hello():
        print("Hello, world!")
    ```

### 4.6 Block Attributes

Block attributes appear in the info string of a fenced code block, after the language identifier. They use a space-separated `key=value` syntax. Boolean attributes (like `run`) have no value.

| Attribute | Type | Applies to | Description |
|-----------|------|------------|-------------|
| `run` | boolean | sh, sql, any lang | Marks the block as executable. |
| `on=<target>` | string | sql, sh | Execution target (database name, SSH host, etc.). |
| `expect=<value>` | string | verify | Expected output for assertion. |
| `model=<model>` | string | ai | AI model to use for this block. |
| `timeout=<seconds>` | integer | all executable | Per-block timeout. Overrides document default. |
| `if={{var}}=<value>` | string | all executable | Conditional: execute only if variable equals value. |
| `pipe` | boolean | all executable | Receives previous block's output as `{{$prev}}`. |
| `id=<identifier>` | string | all | Unique block identifier for cross-referencing and logging. |
| `name=<label>` | string | all executable | Human-readable label for the block (shown in logs and UI). |
| `env=<key=val,...>` | string | sh, sql | Additional environment variables for execution. |
| `cwd=<path>` | string | sh | Working directory for shell execution. |
| `approve` | boolean | all executable | Requires explicit user approval before execution. |
| `watch=<seconds>` | integer | sh | Re-execute on an interval (seconds); live-update output. |
| `on_fail=<action>` | string | all executable | Action on failure: `stop` (default), `continue`, or `retry`. |
| `idempotent` | boolean | all executable | Declares the block safe to re-run without side effects. |

**Attribute Parsing Rules:**
1. The first word of the info string is the language identifier (per CommonMark).
2. Remaining tokens are parsed as `.wia` attributes.
3. Tokens without `=` are boolean attributes (value is `true`).
4. Values containing spaces MUST be quoted with double quotes: `name="Deploy to prod"`.
5. Unknown attributes MUST be ignored (forward compatibility).

---

## 5. Variables

Variables provide dynamic value injection into executable blocks and document text.

### 5.1 Input Variables (`{{name}}`)

Variables declared in front-matter `inputs` are referenced with double-curly-brace syntax: `{{name}}`.

**Resolution Order:**
1. Runtime prompts the user for values before first execution (or uses defaults).
2. Values MAY be provided via CLI arguments, environment variables, or API.
3. If no value is provided and no default exists, the runtime MUST prompt before execution.

**Substitution Scope:**
- Variable substitution MUST occur in executable block content before execution.
- Variable substitution SHOULD occur in non-executable text for display purposes.
- Variable substitution MUST NOT alter the source file on disk.

**Example:**

```yaml
inputs:
  region:
    type: enum
    of: [us-east-1, eu-west-1, ap-northeast-2]
    default: us-east-1
```

    ```sh run
    aws ec2 describe-instances --region {{region}} --output table
    ```

### 5.2 Special Variables

Special variables are built-in and always available. They begin with `$`.

| Variable | Type | Description |
|----------|------|-------------|
| `{{$prev}}` | string | Standard output of the most recently executed block. Empty if no block has run. |
| `{{$prev.exit}}` | integer | Exit code of the most recently executed block. |
| `{{$timestamp}}` | string | Current timestamp in ISO 8601 format (`2026-05-27T14:30:00Z`). |
| `{{$date}}` | string | Current date in ISO 8601 format (`2026-05-27`). |
| `{{$hostname}}` | string | Hostname of the machine executing the block. |
| `{{$user}}` | string | Username of the current user. |
| `{{$os}}` | string | Operating system identifier (`linux`, `darwin`, `win32`). |
| `{{$wia.version}}` | string | `.wia` format version of the current document. |
| `{{$block.index}}` | integer | Zero-based index of the current executable block. |

**Rules:**
- Special variables MUST be resolved at execution time, not at parse time.
- `{{$prev}}` MUST be empty string if no block has been executed in the current session.
- A runtime MUST NOT fail on an unrecognized `{{$...}}` variable; it SHOULD leave it unsubstituted and emit a warning.

---

## 6. Multimodal Extensions

### 6.1 AI Vision Images (`{ai:vision}`)

Images annotated with `{ai:vision}` are flagged for AI visual analysis.

**Syntax:**
```
![alt text](path/to/image.png){ai:vision}
```

**Behavior:**
- The runtime MUST include the referenced image in the context sent to AI blocks that follow it.
- The image MUST be sent as a vision-capable input (base64 or URL) to models that support multimodal input.
- If the AI model does not support vision, the runtime SHOULD send the alt text as a textual fallback.
- Supported image formats: PNG, JPEG, WebP, GIF, SVG. Support for video and audio frames is OPTIONAL.

### 6.2 Source Attribution (`> src: URL`)

Blockquotes prefixed with `src:` provide provenance for claims in the document.

**Syntax:**
```
> src: https://kubernetes.io/docs/reference/kubectl/
```

**Behavior:**
- The runtime SHOULD render the source as a clickable link with a visual badge (e.g., a "Source" label).
- The runtime SHOULD pass source URLs to AI models as context for fact-checking.
- Multiple `> src:` lines MAY appear consecutively to cite multiple sources.
- A `> src:` line MUST be associated with the nearest preceding content block (paragraph, heading, list, or code block).

### 6.3 AI Audio (`{ai:audio}`) — OPTIONAL

```
![meeting recording](meeting.mp3){ai:audio}
```

When supported, the runtime SHOULD transcribe the audio and make the transcript available to subsequent AI blocks via `{{$prev}}`.

---

## 7. Input Types

Input variables declared in front-matter `inputs` MUST specify a `type`. The runtime MUST validate user-provided values against the declared type before execution.

### 7.1 `string`

The default type. Accepts any UTF-8 string.

```yaml
inputs:
  name:
    type: string
    default: "world"
    description: Name to greet
```

### 7.2 `number`

Accepts integer or floating-point values.

```yaml
inputs:
  port:
    type: number
    default: 8080
    description: Server port
```

The runtime MUST reject non-numeric input. The runtime MAY support optional `min` and `max` constraints:

```yaml
inputs:
  replicas:
    type: number
    default: 3
    min: 1
    max: 100
```

### 7.3 `boolean`

Accepts `true` or `false`.

```yaml
inputs:
  dry_run:
    type: boolean
    default: true
    description: Preview changes without applying
```

The runtime SHOULD render this as a toggle or checkbox in the UI.

### 7.4 `enum`

Accepts one of a predefined set of values, specified with the `of` array.

```yaml
inputs:
  environment:
    type: enum
    of: [development, staging, production]
    default: staging
    description: Target deployment environment
```

The runtime MUST reject values not in the `of` array. The runtime SHOULD render this as a dropdown or radio group.

### 7.5 `secret`

Accepts a string that MUST be treated as sensitive.

```yaml
inputs:
  api_key:
    type: secret
    description: API authentication key
```

**Secret handling rules:**
1. The runtime MUST mask secret values in all UI displays (e.g., `********`).
2. Secret values MUST NOT appear in execution logs (S9).
3. Secret values MUST NOT be written to disk in plaintext.
4. Secret values SHOULD be sourced from the system keychain, environment variables, or a secrets manager when available.
5. When passed to shell blocks, secrets SHOULD be injected via environment variables rather than command-line arguments (to avoid `/proc` and `ps` exposure).

### 7.6 `file`

Accepts a file path. The runtime SHOULD provide a file picker UI.

```yaml
inputs:
  config:
    type: file
    description: Configuration file to upload
```

### 7.7 `array`

Accepts a list of values. The `items` field specifies the element type.

```yaml
inputs:
  servers:
    type: array
    items: string
    description: List of server hostnames
```

---

## 8. Execution Model

### 8.1 No Auto-Execution Rule

A conforming runtime MUST NOT execute any block automatically when a document is opened, loaded, or previewed. This is a **security-critical requirement**. Execution MUST require one of:

- User clicking a "Run" control on a specific block.
- User invoking a "Run All" command.
- User executing via CLI with an explicit run flag (e.g., `wia run file.wia`).
- API call with explicit execution intent.

Rationale: `.wia` files may be received from untrusted sources. Auto-execution would create a vector for arbitrary code execution.

### 8.2 Run / Run All

- **Run (single block)**: Executes one block. Variable substitution and `{{$prev}}` resolution occur in the context of previously executed blocks in the current session.
- **Run All**: Executes all executable blocks in document order (S8.3). The runtime MUST stop on the first `verify` FAIL unless the user has opted into "continue on failure" mode.

### 8.3 Sequential Execution Order

Executable blocks are numbered in document order, starting at index 0. When "Run All" is invoked:

1. Blocks execute sequentially, top to bottom.
2. Each block waits for the previous block to complete before starting.
3. `{{$prev}}` is updated after each block completes.
4. Conditional blocks (S8.5) are evaluated and skipped if the condition is false.
5. The runtime MAY support parallel execution of blocks explicitly marked as independent (future extension).

### 8.4 Block Chaining

Blocks with the `pipe` attribute automatically receive the previous block's output.

    ```sh run
    cat /var/log/syslog | tail -50
    ```

    ```ai pipe
    Summarize the key events in this log and flag any anomalies.
    ```

The second block receives the output of the first block as `{{$prev}}`. The `pipe` attribute is syntactic sugar for explicitly writing `{{$prev}}` in the block content—both are equivalent.

### 8.5 Conditional Execution

Blocks with the `if` attribute execute only when the condition is met.

    ```sh run if={{environment}}=production
    kubectl apply -f production-config.yaml
    ```

**Condition syntax:** `if={{variable}}=value`

- The runtime MUST resolve the variable and compare it (case-sensitive string equality) to the value.
- If the condition is false, the block is skipped. Skipped blocks MUST be recorded in the execution log with status `skipped`.
- Negation: `if={{variable}}!=value` (not equal).
- Multiple conditions are not supported in v1. Use separate blocks or shell-level conditionals.

---

## 9. Execution Log

Every block execution produces a log entry. The execution log provides an audit trail for compliance, debugging, and reproducibility.

### 9.1 Log Entry Schema

Each log entry MUST contain the following fields:

```json
{
  "blockId": "string -- block id attribute or auto-generated index (e.g., block-0)",
  "blockName": "string | null -- block name attribute if provided",
  "type": "string -- block type: sh, sql, ai, verify",
  "command": "string -- the executed content (with variables resolved, secrets redacted)",
  "timestamp": "string -- ISO 8601 execution start time",
  "duration_ms": "integer -- execution duration in milliseconds",
  "exitCode": "integer | null -- process exit code (null for ai blocks)",
  "stdout": "string -- captured standard output (truncated at 64 KB)",
  "stderr": "string -- captured standard error (truncated at 64 KB)",
  "pass": "boolean | null -- PASS/FAIL for verify blocks, null for others",
  "expected": "string | null -- expected value for verify blocks",
  "actual": "string | null -- actual output for verify blocks",
  "actor": "string -- who triggered: human, ai, or model identifier",
  "variables": "object -- resolved variable values at execution time (secrets redacted)",
  "skipped": "boolean -- true if block was skipped due to conditional",
  "target": "string | null -- execution target (e.g., database name, SSH host)"
}
```

### 9.2 Compliance Evidence

The execution log of a `.wia` document serves as compliance evidence. For audit purposes:

- The runtime SHOULD support exporting the log as JSON or CSV.
- The runtime SHOULD support cryptographic hashing (SHA-256) of log entries for tamper detection.
- Verify block results (PASS/FAIL) provide automated evidence of control validation.
- The runtime SHOULD record the document's SHA-256 hash at execution start to bind the log to a specific document version.

### 9.3 Log Storage

- Logs SHOULD be stored alongside the document as `<filename>.wia.log` (JSON Lines format, one entry per line).
- The runtime MAY additionally store logs in a database or remote service.
- Logs MUST NOT contain secret variable values (S7.5). Secret values MUST be replaced with `[REDACTED]`.
- Logs SHOULD be rotated or archived when they exceed 10 MB.

---

## 10. Security Model

### 10.1 Permission Scopes

A runtime SHOULD implement a permission system for executable blocks. The RECOMMENDED scopes are:

| Scope | Description | Default |
|-------|-------------|---------|
| `shell.read` | Execute read-only shell commands (`ls`, `cat`, `grep`, etc.) | Allowed |
| `shell.write` | Execute commands that modify the filesystem | Prompt |
| `shell.admin` | Execute commands requiring elevated privileges (`sudo`, `systemctl`) | Prompt |
| `network` | Execute commands that make network requests | Prompt |
| `sql.read` | Execute SELECT queries | Allowed |
| `sql.write` | Execute INSERT/UPDATE/DELETE queries | Prompt |
| `sql.ddl` | Execute CREATE/DROP/ALTER statements | Deny |
| `ai` | Send prompts to AI models | Allowed |

"Prompt" means the runtime MUST ask the user for permission before first execution in the session. "Deny" means the runtime MUST refuse unless the user explicitly overrides.

### 10.2 Secret Variables

See S7.5 for secret handling rules. Additionally:

- The runtime MUST NOT include secret values in AI prompts unless the user explicitly opts in.
- The runtime MUST NOT transmit secret values over unencrypted channels.
- The runtime SHOULD clear secret values from memory after the execution session ends.

### 10.3 Execution Sandboxing

- The runtime SHOULD support executing shell blocks in a sandboxed environment (e.g., container, VM, chroot).
- The runtime MAY provide a "dry run" mode that shows what would execute without running it.
- The runtime MUST respect system-level security policies (SELinux, AppArmor, etc.).

### 10.4 Trust Levels

The `trust` front-matter field declares the intended execution environment:

| Level | Description | Security Posture |
|-------|-------------|-----------------|
| `local` | Executes on the user's local machine | Standard permissions |
| `remote` | Executes on a remote server via SSH | Requires authenticated connection |
| `cloud` | Executes via cloud APIs | Requires API credentials, network access |

The runtime SHOULD display the trust level prominently and SHOULD apply stricter permission defaults for `remote` and `cloud` documents.

---

## 11. Agent Directives

The `agent` front-matter field configures AI behavior for the document.

### 11.1 Agent Role

```yaml
agent:
  role: Senior DevOps engineer specializing in Kubernetes
```

The role string is prepended to AI block prompts as system context. It shapes the AI's persona, expertise level, and communication style for the document.

### 11.2 Agent Rules

```yaml
agent:
  rules:
    - Always explain commands before executing them
    - Never suggest destructive operations without explicit confirmation
    - Cite sources for all factual claims
    - Respond in the document's primary language
```

Rules are constraints that the runtime MUST include in the system prompt for all AI blocks. They act as guardrails for AI behavior within the document context.

### 11.3 Agent Model Selection

```yaml
agent:
  model: claude-sonnet-4-20250514
```

The model field specifies the default AI model for all `ai` blocks in the document. Individual blocks MAY override this with the `model=` attribute. The runtime MUST fall back to its default model if the specified model is unavailable.

### 11.4 Short-form Agent

For simple cases, `agent` MAY be a plain string interpreted as the role:

```yaml
agent: DevOps tutor
```

This is equivalent to:

```yaml
agent:
  role: DevOps tutor
```

---

## 12. Internationalization

### 12.1 BCP 47 Language Tags

The `lang` front-matter field MUST use a valid BCP 47 language tag. Examples: `en`, `ko`, `ja`, `ar`, `zh-Hans`, `pt-BR`.

The runtime SHOULD use this tag to:
- Set the UI language for runtime chrome (buttons, labels).
- Inform AI models of the expected response language.
- Select appropriate fonts and text rendering.

### 12.2 RTL Support

When `lang` specifies a right-to-left language (e.g., `ar`, `he`, `fa`), the runtime SHOULD:
- Render body text with RTL direction.
- Keep code blocks LTR (code is always LTR).
- Apply appropriate bidirectional text handling per the Unicode Bidirectional Algorithm.

### 12.3 254 Language Baseline

The reference runtime (WIA SOOM) supports 254 languages for UI and AI interaction. The `.wia` format itself is language-agnostic—document content, variable descriptions, and agent rules MAY be written in any language. A conforming runtime SHOULD support at minimum the languages defined by ISO 639-1.

---

## 13. MIME Type

The MIME type for `.wia` files is:

```
text/vnd.wia
```

Until IANA registration is complete, implementations SHOULD also accept `text/markdown` as a fallback content type for `.wia` files, since every `.wia` file is valid Markdown.

**Character encoding:** UTF-8 (MUST). No BOM.

---

## 14. File Extension

The canonical file extension is `.wia` (lowercase).

- Operating systems SHOULD associate `.wia` with the installed `.wia` runtime.
- Text editors SHOULD apply Markdown syntax highlighting to `.wia` files.
- Version control systems SHOULD treat `.wia` files as text (diffable, mergeable).
- A file with `.wia` extension but no `wia:` front-matter key MUST still be treated as a valid `.wia` document (Level 0).

---

## 15. Ecosystem

### 15.1 Reference Runtime: WIA SOOM

WIA SOOM is the reference implementation of the `.wia` runtime. It provides:
- Full Level 3 conformance (rendering, execution, AI, verification).
- Cross-platform support (Windows, macOS, Linux) via Electron.
- Integrated SSH terminal, SFTP, and AI assistant (Soomy).
- Execution log with compliance evidence export.
- 254-language UI.

Website: [https://wiasoom.com](https://wiasoom.com)

### 15.2 VS Code Extension (planned)

A VS Code extension providing:
- Syntax highlighting for `.wia` block attributes.
- "Run" CodeLens above executable blocks.
- Execution log panel.
- Variable input sidebar.

### 15.3 CLI Runner (planned: `npx wia run`)

A command-line tool for executing `.wia` documents non-interactively:

```bash
npx wia run deploy.wia --input region=us-east-1 --input dry_run=true
```

Features:
- Headless execution of all blocks.
- JSON log output to stdout.
- Exit code reflects verify block results (0 = all pass, 1 = any fail).
- CI/CD integration.

### 15.4 Web Viewer (planned)

A browser-based renderer at `https://wiasoom.com/view` that:
- Renders `.wia` documents with full visual fidelity.
- Displays executable blocks with syntax highlighting and visual indicators.
- Does NOT execute blocks (security: web viewer is Level 1 only).
- Provides an "Open in WIA SOOM" deep link for execution.

### 15.5 Pandoc Integration (planned)

A Pandoc reader/writer for `.wia` enabling conversion:
- `.wia` to HTML, PDF, DOCX (preserving block metadata as annotations).
- Markdown to `.wia` (adding front-matter and detecting executable patterns).

---

## 16. Grammar (Informal)

The following EBNF-like grammar describes the `.wia`-specific extensions. This does NOT describe CommonMark itself (see the CommonMark spec for that).

```ebnf
wia_document    = [ front_matter ] body ;

front_matter    = "---" NEWLINE yaml_content NEWLINE "---" NEWLINE ;
yaml_content    = (* valid YAML 1.2 with required 'wia' key *) ;

body            = { block | commonmark_content } ;

block           = fence_open NEWLINE block_content NEWLINE fence_close ;
fence_open      = "```" info_string ;
fence_close     = "```" ;
info_string     = language { SPACE attribute } ;
language        = IDENTIFIER ;

attribute       = bool_attr | kv_attr ;
bool_attr       = IDENTIFIER ;                          (* e.g., "run", "pipe" *)
kv_attr         = IDENTIFIER "=" value ;                (* e.g., "on=mydb" *)
value           = QUOTED_STRING | UNQUOTED_TOKEN ;

variable        = "{{" var_name "}}" ;
var_name        = "$" IDENTIFIER [ "." IDENTIFIER ]     (* special variables *)
                | IDENTIFIER ;                          (* input variables *)

ai_image_attr   = "{ai:" IDENTIFIER "}" ;               (* e.g., {ai:vision} *)

source_line     = "> src:" SPACE URL ;

IDENTIFIER      = LETTER { LETTER | DIGIT | "_" | "-" | "." } ;
UNQUOTED_TOKEN  = { PRINTABLE - SPACE } ;
QUOTED_STRING   = '"' { PRINTABLE - '"' } '"' ;
```

---

## 17. Examples

### 17.1 Minimal `.wia` Document

    ---
    wia: "1"
    ---

    # Hello, WIA

    This is the simplest possible `.wia` document.

### 17.2 DevOps Runbook

    ---
    wia: "1"
    title: Kubernetes Deployment Rollback
    lang: en
    agent:
      role: SRE on-call engineer
      rules:
        - Explain each step before execution
        - Always check pod health after rollback
    inputs:
      namespace:
        type: string
        default: production
      deployment:
        type: string
        description: Name of the deployment to roll back
    tags: [k8s, rollback, incident-response]
    timeout: 120
    ---

    # Deployment Rollback Procedure

    ## Step 1: Check current deployment status

    ```sh run
    kubectl rollout status deployment/{{deployment}} -n {{namespace}}
    ```

    ## Step 2: View rollout history

    ```sh run
    kubectl rollout history deployment/{{deployment}} -n {{namespace}}
    ```

    ## Step 3: Roll back to previous revision

    ```sh run
    kubectl rollout undo deployment/{{deployment}} -n {{namespace}}
    ```

    ## Step 4: Verify rollback succeeded

    ```verify expect=True
    kubectl rollout status deployment/{{deployment}} -n {{namespace}} \
      | grep -q "successfully rolled out" && echo True || echo False
    ```

    ## Step 5: AI incident summary

    ```ai pipe
    Based on the deployment rollback output above, write a brief incident
    summary including: what was rolled back, whether it succeeded, and
    recommended follow-up actions.
    ```

### 17.3 AI-Assisted Tutorial

    ---
    wia: "1"
    title: Introduction to Docker
    lang: en
    agent: Friendly programming tutor who explains concepts step by step
    inputs:
      skill_level:
        type: enum
        of: [beginner, intermediate, advanced]
        default: beginner
    ---

    # Docker Tutorial

    ## Check Docker installation

    ```sh run
    docker --version
    ```

    ## Your first container

    ```sh run
    docker run --rm hello-world
    ```

    ## Understanding the output

    ```ai
    The student (skill level: {{skill_level}}) just ran their first Docker
    container. Explain what happened in the output above, step by step.
    Use analogies appropriate for their skill level.

    {{$prev}}
    ```

### 17.4 Compliance Audit

    ---
    wia: "1"
    title: SOC 2 -- Access Control Verification
    lang: en
    agent:
      role: Compliance auditor
      rules:
        - Report findings factually
        - Flag any control failure as CRITICAL
    tags: [compliance, soc2, access-control]
    ---

    # SOC 2 Access Control Audit

    ## AC-1: SSH root login is disabled

    ```verify expect=no
    grep "^PermitRootLogin" /etc/ssh/sshd_config | awk '{print $2}'
    ```

    ## AC-2: Password authentication is disabled

    ```verify expect=no
    grep "^PasswordAuthentication" /etc/ssh/sshd_config | awk '{print $2}'
    ```

    ## AC-3: No users have empty passwords

    ```verify expect=0
    awk -F: '($2 == "") {count++} END {print count+0}' /etc/shadow
    ```

    ## AC-4: Firewall is active

    ```verify expect=active
    ufw status | head -1 | awk '{print $2}'
    ```

    ## Summary

    ```ai
    Review the verification results above and produce a compliance summary
    table with columns: Control ID, Description, Status, Finding.
    Flag any FAIL results as requiring immediate remediation.
    ```

### 17.5 Multi-Language Data Pipeline

    ---
    wia: "1"
    title: Multi-Language Data Pipeline
    lang: ko
    agent:
      role: Data engineer
      model: gpt-4o
    inputs:
      source_db:
        type: string
        default: analytics_prod
        description: Source database
      target_date:
        type: string
        default: "{{$date}}"
        description: Target date (YYYY-MM-DD)
    tags: [data-pipeline, etl]
    ---

    # Daily Data Pipeline

    ## Step 1: Check source data

    ```sql run on={{source_db}}
    SELECT COUNT(*) as total_records,
           MIN(created_at) as earliest,
           MAX(created_at) as latest
    FROM events
    WHERE DATE(created_at) = '{{target_date}}';
    ```

    ## Step 2: Data quality verification

    ```verify expect=0
    psql -d {{source_db}} -t -c \
      "SELECT COUNT(*) FROM events WHERE DATE(created_at) = '{{target_date}}' AND user_id IS NULL;"
    ```

    > src: https://www.postgresql.org/docs/current/functions-datetime.html

    ## Step 3: AI analysis

    ```ai pipe
    Analyze the data quality verification results above.
    If anomalies exist, explain causes and suggest remediation.
    ```

---

## 18. Comparison with Existing Formats

| Feature | .wia | Jupyter | Quarto | RUNME | Org-mode | AGENTS.md |
|---------|------|---------|--------|-------|----------|-----------|
| Plain text | Yes | No (JSON) | Yes | Yes | Yes | Yes |
| Valid Markdown | Yes | No | Yes | Yes | No | Yes |
| Shell execution | Yes | Yes | Yes | Yes | Yes | No |
| SQL execution | Yes | via kernel | via knitr | No | Yes | No |
| AI-native blocks | Yes | No | No | No | No | context only |
| Built-in verification | Yes | No | No | No | No | No |
| Multimodal (AI vision) | Yes | display only | display only | No | No | No |
| Source attribution | Yes | No | No | No | No | No |
| Typed inputs | Yes | via widgets | Yes | No | No | No |
| Secret handling | Yes | No | No | No | No | No |
| Execution log / audit | Yes | in-cell | No | No | No | No |
| VCS-friendly diff | Yes | No | Yes | Yes | Yes | Yes |
| Language-agnostic | Yes | No (Python) | No (R/Python) | Yes | Yes | Yes |
| No vendor lock-in | Yes | No (kernel) | No (Quarto CLI) | No (VS Code) | No (Emacs) | Yes |
| i18n (254 languages) | Yes | No | No | No | No | No |

---

## 19. Future Extensions (v2+)

The following features are under consideration for future versions. They are explicitly **out of scope** for v1.

1. **Transclusion (`@include`)** — Include content from other `.wia` or Markdown files:

       @include(./shared/auth-check.wia)

2. **Cryptographic Signing** — Sign documents and execution logs for non-repudiation:

       signed-by: sha256:abc123...

3. **Collaborative Merge** — Semantic merge strategies for concurrent edits to `.wia` documents, preserving execution log integrity.

4. **Block Dependency Graphs** — Declare explicit dependencies between blocks for parallel execution:

       ```sh run id=fetch depends=setup
       ```

5. **Bidirectional Export** — `.wia` to/from HTML/PDF with round-trip fidelity, preserving executable block metadata in HTML data attributes or PDF annotations.

6. **Live Blocks** — Blocks that re-execute on a schedule or on file change:

       ```sh run interval=30s
       kubectl get pods -n production
       ```

7. **Remote Collaboration** — Real-time collaborative editing with execution state synchronization.

8. **Block Output Formats** — Structured output declarations (table, chart, JSON, image):

       ```sh run output=table
       ```

---

## Appendix A: JSON Schema for Front-matter

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://wiasoom.com/schemas/wia-v1.json",
  "title": ".wia Front-matter Schema v1",
  "type": "object",
  "required": ["wia"],
  "properties": {
    "wia": {
      "type": "string",
      "const": "1",
      "description": "Format version. Must be 1 for this specification."
    },
    "title": {
      "type": "string",
      "description": "Human-readable document title."
    },
    "lang": {
      "type": "string",
      "pattern": "^[a-zA-Z]{2,3}(-[a-zA-Z0-9]+)*$",
      "default": "en",
      "description": "Primary language (BCP 47 tag)."
    },
    "agent": {
      "oneOf": [
        { "type": "string" },
        {
          "type": "object",
          "properties": {
            "role": {
              "type": "string",
              "description": "AI persona / expertise description."
            },
            "rules": {
              "type": "array",
              "items": { "type": "string" },
              "description": "Behavioral constraints for AI blocks."
            },
            "model": {
              "type": "string",
              "description": "Default AI model identifier."
            }
          }
        }
      ],
      "description": "AI agent configuration."
    },
    "inputs": {
      "type": "object",
      "additionalProperties": {
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "enum": ["string", "number", "boolean", "enum", "secret", "file", "array"],
            "default": "string"
          },
          "default": {
            "description": "Default value."
          },
          "of": {
            "type": "array",
            "items": { "type": "string" },
            "description": "Allowed values (required for enum type)."
          },
          "description": {
            "type": "string",
            "description": "Human-readable description."
          },
          "min": { "type": "number" },
          "max": { "type": "number" },
          "items": {
            "type": "string",
            "description": "Element type for array inputs."
          }
        },
        "required": ["type"]
      },
      "description": "Typed input parameters."
    },
    "outputs": {
      "type": "object",
      "additionalProperties": {
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "enum": ["file", "string", "json"]
          },
          "path": { "type": "string" },
          "description": { "type": "string" }
        }
      },
      "description": "Declared output artifacts."
    },
    "tags": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Classification tags."
    },
    "timeout": {
      "type": "integer",
      "minimum": 1,
      "default": 30,
      "description": "Default execution timeout in seconds."
    },
    "trust": {
      "type": "string",
      "enum": ["local", "remote", "cloud"],
      "default": "local",
      "description": "Intended execution environment."
    },
    "$schema": {
      "type": "string",
      "format": "uri",
      "description": "JSON Schema URL for validation."
    }
  },
  "additionalProperties": true
}
```

---

## Appendix B: MIME Type Registration Template

Per RFC 6838, the following template is prepared for IANA registration:

```
Type name: text
Subtype name: vnd.wia
Required parameters: none
Optional parameters:
  charset -- MUST be "UTF-8" if specified.
Encoding considerations: 8bit (UTF-8)
Security considerations:
  .wia documents may contain executable blocks (shell commands,
  SQL queries, AI prompts). Implementations MUST NOT auto-execute
  any content. Execution requires explicit user action. See S10.
Interoperability considerations:
  .wia is a strict superset of CommonMark Markdown. Any Markdown
  renderer can display .wia files. Only .wia-aware runtimes can
  execute embedded blocks.
Published specification: https://wiasoom.com/spec/wia-v1
Applications which use this media type:
  WIA SOOM (https://wiasoom.com)
Fragment identifier considerations: none
Additional information:
  File extension: .wia
  Macintosh file type code: none
  Object identifier: none
Person and email address to contact for further information:
  SmileStory Inc. <wiasoom@gmail.com>
Intended usage: COMMON
Restrictions on usage: none
Author: SmileStory Inc.
Change controller: SmileStory Inc.
```

---

## Appendix C: Glossary

| Term | Definition |
|------|-----------|
| **Actor** | The entity that initiated a block execution: `human` (user action), `ai` (AI-triggered), or a model identifier (e.g., `claude-sonnet-4-20250514`). |
| **Block** | A fenced code block in the document, optionally annotated with `.wia` attributes. |
| **Block attribute** | A key or key-value pair in a fenced code block's info string that controls `.wia` behavior (e.g., `run`, `on=mydb`, `pipe`). |
| **CommonMark** | The standard, unambiguous specification for Markdown. Version 0.31.2 is the baseline for `.wia` v1. |
| **Display block** | A fenced code block without execution attributes. Rendered as static code. |
| **Executable block** | A fenced code block with `run`, `ai`, or `verify` attributes. Can be executed by a conforming runtime. |
| **Execution log** | A structured record of all block executions in a session, including inputs, outputs, timing, and results. |
| **Front-matter** | A YAML block at the start of the document, delimited by `---`, containing document metadata. |
| **Info string** | The text after the opening fence of a code block (e.g., `sh run timeout=30`). |
| **Input variable** | A typed parameter declared in front-matter `inputs` and referenced as `{{name}}` in the document. |
| **Level (conformance)** | One of four implementation tiers: Level 0 (renderer), Level 1 (reader), Level 2 (runner), Level 3 (full). |
| **Renderer** | Software that displays `.wia` as formatted text. Any CommonMark renderer qualifies as Level 0. |
| **Runner** | The execution engine for a block type (e.g., shell for `sh`, database client for `sql`, LLM API for `ai`). |
| **Runtime** | Software that interprets and executes `.wia` extensions. The reference runtime is WIA SOOM. |
| **Secret** | An input variable of type `secret` that MUST be masked in display and redacted in logs. |
| **Special variable** | A built-in variable prefixed with `$` (e.g., `{{$prev}}`, `{{$timestamp}}`). |
| **Trust level** | The declared execution environment (`local`, `remote`, `cloud`) that influences security defaults. |
| **Verify block** | An executable block that asserts its output matches an expected value, producing PASS or FAIL. |

---

*This specification is maintained by SmileStory Inc. and the WIA SOOM community.*
*Contributions, issues, and discussions: [https://github.com/WIA-Official/wia-soom](https://github.com/WIA-Official/wia-soom)*

*Copyright 2026 SmileStory Inc. Released under CC BY 4.0.*
