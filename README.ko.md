# `.wia` — AI 네이티브 문서 포맷

**언어:** [English](README.md) · 한국어 · [中文](README.zh.md) · [日本語](README.ja.md) · [Español](README.es.md) · [العربية](README.ar.md)

> **사람이 쓰고, AI가 실행하고, 기계가 검증하고, 로봇이 수렴한다.**

`.wia`는 마크다운의 상위집합입니다. 모든 `.md`는 그대로 유효한 `.wia`예요.
마크다운이 못 하는 것을 `.wia`가 더합니다 — 딱 그만큼만.

```
Markdown  = 읽기
.wia      = 읽기 + 실행 + 검증 + AI + 피지컬 AI + IoT
```

---

## 모두가 기다려 온 포맷

다섯 가지를 모두 갖춘 포맷은 없었습니다:

|            | 사람이 읽음 | 실행 가능 | AI 네이티브 | 자기검증 | 피지컬 AI |
| ---------- | ----------- | --------- | ----------- | -------- | --------- |
| Markdown   | ✅           | ❌         | ❌           | ❌        | ❌         |
| Jupyter    | ❌ (JSON)    | ✅         | ❌           | ❌        | ❌         |
| AGENTS.md  | ✅           | ❌         | ✅           | ❌        | ❌         |
| Terraform  | ❌           | ✅         | ❌           | △        | ❌         |
| Ansible    | ❌ (YAML)    | ✅         | △           | ❌        | ❌         |
| RUNME      | ✅           | ✅         | ❌           | ❌        | ❌         |
| **`.wia`** | **✅**       | **✅**     | **✅**       | **✅**    | **✅**     |

---

## 45개+ 포맷이 .wia로 변환됩니다

`.wia`는 **상위집합**입니다 — 아래 모든 것을 끌어올릴 수 있어요:

**문서 · 설정**: `.md` · `.txt` · `.rst` · `.adoc` · `.json` · `.yml` · `.toml` · `.ini` · `.xml` · `.env` · `.properties` · `.plist` · `.csv` · `.log`

**프로그래밍**: `.sh` · `.py` · `.sql` · `.js` · `.ts` · `.go` · `.rs` · `.rb` · `.java` · `.c` · `.cpp` · `.lua` · `.ps1`

**인프라**: `.tf` · `.hcl` · `Dockerfile` · `docker-compose.yml` · `Jenkinsfile` · `.gradle` · `Vagrantfile` · `Makefile` · `crontab` · `nginx.conf`

**API · 스키마**: `.proto` · `.graphql` · `.prisma`

**데이터 과학**: `.ipynb` (Jupyter → .wia 블록 변환)

**접근성**: `.brf` · `.brl` (점자)

---

## 기능

### 블록 타입
`sh run` · `sql run on=` · `ai [model=]` · `verify expect=` · `python run` · `node run` · `display`

### 블록 속성
`run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` · `pipe` · `retry=` · `converge=` · `drift=`

### 입력 타입
`string` · `number` · `boolean` · `enum` · `secret` · `file` · `array`

### 특수 변수
`{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` · `{{$os}}` · `{{$arch}}`

### 안전성
승인 게이트 · 드라이런 모드 · 롤백(`on_fail=`) · 멱등성 · 비밀값 마스킹 · 셸 인젝션 방지

### AI 통합
Soomy 자동 에이전트 · 모델 선택 · 비전 이미지 · 결과 AI 분석 · AI가 .wia 생성("런북 만들어줘")

### 컴플라이언스
실행 로그(감사 추적) · HTML 리포트 내보내기 · SOC 2 / ISO 27001 / ISO 9001 증거 생성(**자동 통제 22개** — SOC 2 9개, ISO 27001 8개, ISO 9001 5개)

---

## 254개 언어 어느 것으로든 작성됩니다

`.wia`는 평문 UTF-8 텍스트입니다. 작성자는 자기 언어로 쓰고, 런타임은 글의 인간 언어와 무관하게 동일하게 실행합니다.

이건 주장이 아니라 예제에 들어 있어요. 예를 들어 [`examples/server-health.wia`](examples/server-health.wia)는 한국어로 작성됐고(`title: WIA SOOM 서버 건강 점검`), 영어 런북과 똑같이 동작합니다. **254개 언어** 어느 작업자든 모국어로 `.wia`를 읽고 쓰고 실행할 수 있으며, **WIA SOOM** 런타임 UI도 254개 언어로 지역화돼 있습니다.

접근성도 같은 정신으로 기본 탑재했어요: WCAG AA, RTL 문자, 점자(`.brf` / `.brl`), 완전한 키보드 내비게이션. 목표는 하나입니다 — 법정도, 감사관도, 로봇도, 모국어로 일하는 시각장애 작업자도 모두 읽을 수 있는 단 하나의 운영 포맷.

---

## 피지컬 AI · ROS 2 · IoT

`.wia`는 **로봇 플릿 운영**과 **IoT 기기 관리**를 위해 설계됐습니다:

### ROS 2 로봇 관리
- SSH 기반 ROS 2 CLI 브리지(**IPC 27개**)
- 로봇 상태 모니터링(노드, 토픽, 서비스, 배터리, CPU 온도)
- AI 기반 로봇 진단
- ros2 bag 기록 / 재생 / 분석
- 원하는 상태(desired-state) 수렴 엔진 + 설정 드리프트 감지(플릿 전체)
- `.wia` 복구 런북 자동 생성

### IoT 기기 관리
SSH가 되는 리눅스 기기라면 모두 `.wia` 대상입니다: 라즈베리파이 · 스마트팩토리 센서 · 스마트팜 · CCTV/NVR · 네트워크 장비 · 드론 · 자율주행 차량.

### 소프트웨어 vs 하드웨어
`.wia`는 전체 "장애"의 대부분을 차지하는 **소프트웨어 문제**를 원격으로 해결합니다 — 프로세스 중단(재시작), 메모리 문제(정리), 설정 오류(복원), 네트워크 끊김(재연결)을 현장 방문 없이요. 하드웨어 고장(모터·센서 손상)은 사람 손이 필요하지만, 그 경우에도 `.wia`는 진단·예방·수리 후 검증을 돕습니다.

---

## 예제 런북 111개

[`examples/`](examples) 디렉토리에 **실전용 런북 111개**(실측)가 13개 카테고리로 들어 있습니다:

| 카테고리 | 개수 | 예시 |
| -------- | ---- | ---- |
| 🖥️ 서버 / OS | 13 | `amazon-linux-setup.wia`, `ssh-hardening.wia`, `linux-performance-tuning.wia` |
| 🌐 웹 / 앱 | 10 | `nginx-install.wia`, `wordpress-install.wia`, `nodejs-deploy.wia`, `pm2-deploy.wia` |
| 🗄️ 데이터베이스 | 10 | `mysql-install.wia`, `postgresql-backup.wia`, `redis-install.wia`, `mongodb-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`, `docker-compose-deploy.wia`, `docker-registry.wia` |
| ☸️ Kubernetes | 9 | `k8s-cluster-check.wia`, `k8s-rollback.wia`, `helm-install-app.wia` |
| 📊 모니터링 / 로깅 | 9 | `prometheus-install.wia`, `elk-stack-setup.wia`, `log-investigation.wia` |
| 🔒 보안 / 컴플라이언스 | 13 | `security-audit.wia`, `fail2ban-setup.wia`, `ssl-cert-renewal.wia`, `aws-iam-audit.wia` |
| 🔄 CI/CD / IaC | 6 | `github-actions-setup.wia`, `terraform-apply.wia`, `ansible-playbook-run.wia` |
| ☁️ 클라우드 / AWS | 8 | `aws-cli-setup.wia`, `s3-backup.wia`, `ec2-snapshot.wia`, `autoscaling-setup.wia` |
| 🌍 네트워크 / DNS | 6 | `network-troubleshoot.wia`, `dns-troubleshoot.wia`, `site-failover-dns.wia` |
| 📧 통신 | 3 | `postfix-setup.wia`, `smtp-test.wia`, `slack-webhook.wia` |
| 🤖 로봇 / ROS 2 | 10 | `ros-diagnostic.wia`, `ros-node-recovery.wia`, `robot-fleet-health.wia`, `ros2-bag-record.wia` |
| 🏥 장애 / DR | 10 | `high-cpu-response.wia`, `oom-response.wia`, `disk-full-response.wia`, `disaster-recovery-plan.wia` |

---

## 생태계

| 도구 | 역할 | 상태 |
| ---- | ---- | ---- |
| **[WIA SOOM](https://wiasoom.com)** | 레퍼런스 런타임(Win/Mac/Linux) | ✅ v3.9.29 |
| **[Spec v1](SPEC-v1.md)** | 공식 명세(19개 섹션) | ✅ 공개됨 |
| **[런북 111개](examples)** | 실전용 템플릿 | ✅ 제공 중 |
| **[논문 (Zenodo)](https://doi.org/10.5281/zenodo.20448006)** | 인용 가능한 프리프린트 + DOI (CC-BY 4.0) | ✅ 공개됨 |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | 포맷 소개 페이지 | ✅ 운영 중 |
| **[변환기](https://wia.wiasoom.com/convert.html)** | 45개+ 포맷 → .wia | ✅ 운영 중 |
| **[뷰어](https://wia.wiasoom.com/view.html)** | 설치 없이 .wia 읽기 | ✅ 운영 중 |
| **Rust CLI** (`wia`) | 단일 바이너리 변환/실행기 | 🔜 로드맵 |
| **VS Code 확장** | 구문 강조 + 미리보기 | 🔜 로드맵 |

### Rust 툴링 로드맵

```
libwia (Rust 코어 라이브러리)
├── wia CLI      → 단일 바이너리 변환/실행기
├── WASM 모듈    → 브라우저 도구를 네이티브 속도로
└── napi-rs      → Electron 앱 통합
```

---

## 설계 원칙

1. **마크다운 상위집합** — 모든 `.md`는 유효한 `.wia`
2. **사람 우선** — 도구 없이도 읽힘
3. **자동 실행 금지** — 사용자가 직접 Run 클릭(보안)
4. **언어 독립** — 254개 인간 언어, 모든 프로그래밍 언어
5. **이식성** — 평문 텍스트, 벤더 종속 없음
6. **자기검증** — 내장 단언(assertion)
7. **AI 네이티브** — AI가 읽고 실행하고 확장하고 검증
8. **피지컬 AI 대응** — ROS 2 플릿 운영 + IoT
9. **접근성** — WCAG AA, RTL, 점자, 키보드 내비게이션

## 인용

학술·기술 자료에서 `.wia`를 참조하실 때는 프리프린트를 인용해 주세요:

> Yeon, Sam-heum. *.wia: An AI-Native Document Format for Executable, Self-Verifying Operations in Physical AI.* Zenodo, 2026. https://doi.org/10.5281/zenodo.20448006

## MIME 타입

`text/vnd.wia`

## 라이선스

명세: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · 예제: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

제작: **[(주)스마일스토리](https://smilestory.net)** (WIA Standards) · [wiasoom.com](https://wiasoom.com)
