# `.wia` — AI ネイティブ・ドキュメント形式

**言語:** [English](README.md) · [한국어](README.ko.md) · [中文](README.zh.md) · 日本語 · [Español](README.es.md) · [العربية](README.ar.md)

> **人が書き、AI が実行し、機械が検証し、ロボットが収束する。**

`.wia` は Markdown のスーパーセットです。すべての `.md` はそのまま有効な `.wia` です。
Markdown にできないことを `.wia` が補います —— ちょうどそれだけ。

```
Markdown  = 読む
.wia      = 読む + 実行 + 検証 + AI + フィジカル AI + IoT
```

---

## 誰もが待っていた形式

5 つすべてを兼ね備えた既存の形式はありません：

|            | 人が読める | 実行可能 | AI ネイティブ | 自己検証 | フィジカル AI |
| ---------- | ---------- | -------- | ------------- | -------- | ------------- |
| Markdown   | ✅          | ❌        | ❌             | ❌        | ❌             |
| Jupyter    | ❌ (JSON)   | ✅        | ❌             | ❌        | ❌             |
| AGENTS.md  | ✅          | ❌        | ✅             | ❌        | ❌             |
| Terraform  | ❌          | ✅        | ❌             | △        | ❌             |
| Ansible    | ❌ (YAML)   | ✅        | △             | ❌        | ❌             |
| RUNME      | ✅          | ✅        | ❌             | ❌        | ❌             |
| **`.wia`** | **✅**      | **✅**    | **✅**         | **✅**    | **✅**         |

---

## 45+ の形式が .wia に変換できます

`.wia` は**スーパーセット**です —— 以下のすべてを取り込めます：

**ドキュメント・設定**：`.md` · `.txt` · `.rst` · `.adoc` · `.json` · `.yml` · `.toml` · `.ini` · `.xml` · `.env` · `.properties` · `.plist` · `.csv` · `.log`

**プログラミング**：`.sh` · `.py` · `.sql` · `.js` · `.ts` · `.go` · `.rs` · `.rb` · `.java` · `.c` · `.cpp` · `.lua` · `.ps1`

**インフラ**：`.tf` · `.hcl` · `Dockerfile` · `docker-compose.yml` · `Jenkinsfile` · `.gradle` · `Vagrantfile` · `Makefile` · `crontab` · `nginx.conf`

**API・スキーマ**：`.proto` · `.graphql` · `.prisma`

**データサイエンス**：`.ipynb`（Jupyter → .wia ブロック変換）

**アクセシビリティ**：`.brf` · `.brl`（点字）

---

## 機能

### ブロックタイプ
`sh run` · `sql run on=` · `ai [model=]` · `verify expect=` · `python run` · `node run` · `display`

### ブロック属性
`run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` · `pipe` · `retry=` · `converge=` · `drift=`

### 入力タイプ
`string` · `number` · `boolean` · `enum` · `secret` · `file` · `array`

### 特殊変数
`{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` · `{{$os}}` · `{{$arch}}`

### 安全性
承認ゲート · ドライラン · ロールバック（`on_fail=`）· 冪等性 · シークレットのマスキング · シェルインジェクション防止

### AI 統合
Soomy 自動エージェント · モデル選択 · ビジョン画像 · 結果の AI 分析 · AI による .wia 生成（「runbook を作って」）

### コンプライアンス
実行ログ（監査証跡）· HTML レポート出力 · SOC 2 / ISO 27001 / ISO 9001 証跡生成（**22 の自動化コントロール** —— SOC 2 9、ISO 27001 8、ISO 9001 5）

---

## 254 言語のいずれでも記述できます

`.wia` はプレーンな UTF-8 テキストです。著者は自分の言語で書き —— 散文がどの人間言語であっても、ランタイムは同一に実行します。

これは主張ではなく、サンプルに含まれています。例えば [`examples/server-health.wia`](examples/server-health.wia) は韓国語で書かれており（`title: WIA SOOM 서버 건강 점검`）、英語の runbook とまったく同じように動作します。**254 言語**のいずれの現場オペレーターも、母語で `.wia` を読み・書き・実行でき、**WIA SOOM** ランタイム UI も全 254 言語にローカライズされています。

アクセシビリティも同じ精神で組み込まれています：WCAG AA、RTL スクリプト、点字（`.brf` / `.brl`）、完全なキーボードナビゲーション。目標は一つの運用形式 —— 裁判所も、監査人も、ロボットも、母語で働く視覚障害のあるオペレーターも、すべてが読めること。

---

## フィジカル AI、ROS 2 & IoT

`.wia` は**ロボットフリート運用**と **IoT 機器管理**のために構築されています：

### ROS 2 ロボット管理
- SSH ベースの ROS 2 CLI ブリッジ（**27 の IPC エンドポイント**）
- ロボットのヘルス監視（ノード、トピック、サービス、バッテリー、CPU 温度）
- AI によるロボット診断
- ros2 bag の記録 / 再生 / 分析
- 望ましい状態への収束エンジン + 設定ドリフト検出（フリート全体）
- `.wia` 復旧 runbook の自動生成

### IoT 機器管理
SSH が使える Linux 機器ならすべて `.wia` 対応：Raspberry Pi · スマート工場センサー · スマートファーム · CCTV/NVR · ネットワーク機器 · ドローン · 自動運転車。

### ソフトウェア vs ハードウェア
`.wia` は運用「障害」の大多数を占める**ソフトウェア問題**を遠隔で解決します —— プロセスのクラッシュ（再起動）、メモリ問題（クリーンアップ）、設定エラー（復元）、ネットワーク切断（再接続）—— 現地訪問なしで。ハードウェア故障（モーター、センサー破損）は人の手が必要ですが、`.wia` は診断・予防・修理後の検証を支援します。

---

## 111 のサンプル Runbook

[`examples/`](examples) ディレクトリには **111 の本番対応 runbook**（検証済みの数）が 13 カテゴリにわたって含まれています：

| カテゴリ | 数 | 例 |
| -------- | -- | -- |
| 🖥️ サーバー / OS | 13 | `amazon-linux-setup.wia`、`ssh-hardening.wia`、`linux-performance-tuning.wia` |
| 🌐 Web / アプリ | 10 | `nginx-install.wia`、`wordpress-install.wia`、`nodejs-deploy.wia`、`pm2-deploy.wia` |
| 🗄️ データベース | 10 | `mysql-install.wia`、`postgresql-backup.wia`、`redis-install.wia`、`mongodb-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`、`docker-compose-deploy.wia`、`docker-registry.wia` |
| ☸️ Kubernetes | 9 | `k8s-cluster-check.wia`、`k8s-rollback.wia`、`helm-install-app.wia` |
| 📊 監視 / ロギング | 9 | `prometheus-install.wia`、`elk-stack-setup.wia`、`log-investigation.wia` |
| 🔒 セキュリティ / コンプライアンス | 13 | `security-audit.wia`、`fail2ban-setup.wia`、`ssl-cert-renewal.wia`、`aws-iam-audit.wia` |
| 🔄 CI/CD / IaC | 6 | `github-actions-setup.wia`、`terraform-apply.wia`、`ansible-playbook-run.wia` |
| ☁️ クラウド / AWS | 8 | `aws-cli-setup.wia`、`s3-backup.wia`、`ec2-snapshot.wia`、`autoscaling-setup.wia` |
| 🌍 ネットワーク / DNS | 6 | `network-troubleshoot.wia`、`dns-troubleshoot.wia`、`site-failover-dns.wia` |
| 📧 通信 | 3 | `postfix-setup.wia`、`smtp-test.wia`、`slack-webhook.wia` |
| 🤖 ロボット / ROS 2 | 10 | `ros-diagnostic.wia`、`ros-node-recovery.wia`、`robot-fleet-health.wia`、`ros2-bag-record.wia` |
| 🏥 インシデント / DR | 10 | `high-cpu-response.wia`、`oom-response.wia`、`disk-full-response.wia`、`disaster-recovery-plan.wia` |

---

## エコシステム

| ツール | 役割 | 状態 |
| ------ | ---- | ---- |
| **[WIA SOOM](https://wiasoom.com)** | リファレンスランタイム（Win/Mac/Linux） | ✅ v3.9.29 |
| **[Spec v1](SPEC-v1.md)** | 公式仕様（19 セクション） | ✅ 公開済み |
| **[111 Runbook](examples)** | 本番対応テンプレート | ✅ 利用可能 |
| **[論文 (Zenodo)](https://doi.org/10.5281/zenodo.20448006)** | 引用可能なプレプリント + DOI (CC-BY 4.0) | ✅ 公開済み |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | 形式ランディングページ | ✅ 公開中 |
| **[コンバーター](https://wia.wiasoom.com/convert.html)** | 45+ 形式 → .wia | ✅ 公開中 |
| **[ビューア](https://wia.wiasoom.com/view.html)** | インストール不要で .wia を閲覧 | ✅ 公開中 |
| **Rust CLI** (`wia`) | 単一バイナリの変換/実行ツール | 🔜 ロードマップ |
| **VS Code 拡張** | シンタックスハイライト + プレビュー | 🔜 ロードマップ |

### Rust ツールチェーン・ロードマップ

```
libwia (Rust コアライブラリ)
├── wia CLI      → 単一バイナリの変換/実行ツール
├── WASM モジュール → ネイティブ速度のブラウザツール
└── napi-rs      → Electron アプリ統合
```

---

## 設計原則

1. **Markdown スーパーセット** —— すべての `.md` は有効な `.wia`
2. **人間優先** —— ツールなしで読める
3. **自動実行なし** —— ユーザーが Run をクリックする必要あり（セキュリティ）
4. **言語非依存** —— 254 の人間言語、任意のプログラミング言語
5. **可搬性** —— プレーンテキスト、ベンダーロックインなし
6. **自己検証** —— 組み込みアサーション
7. **AI ネイティブ** —— AI が読み・実行・拡張・検証
8. **フィジカル AI 対応** —— ROS 2 フリート運用 + IoT
9. **アクセシブル** —— WCAG AA、RTL、点字、キーボードナビゲーション

## 引用

学術・技術的な著作で `.wia` を参照する場合は、プレプリントを引用してください：

> Yeon, Sam-heum. *.wia: An AI-Native Document Format for Executable, Self-Verifying Operations in Physical AI.* Zenodo, 2026. https://doi.org/10.5281/zenodo.20448006

## MIME タイプ

`text/vnd.wia`

## ライセンス

仕様：[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · サンプル：[Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

作成：**[Smilestory Co., Ltd.](https://smilestory.net)**（WIA Standards） · [wiasoom.com](https://wiasoom.com)
