<div dir="rtl">

# `.wia` — صيغة المستندات الأصلية للذكاء الاصطناعي

**اللغة:** [English](README.md) · [한국어](README.ko.md) · [中文](README.zh.md) · [日本語](README.ja.md) · [Español](README.es.md) · العربية

> **البشر يكتبون. الذكاء الاصطناعي ينفّذ. الآلات تتحقّق. الروبوتات تتقارب.**

`.wia` هي مجموعة شاملة (superset) من Markdown. كل ملف `.md` هو `.wia` صالح.
ما لا يستطيع Markdown فعله، تضيفه `.wia` —— ولا شيء أكثر من ذلك.

```
Markdown  = قراءة
.wia      = قراءة + تنفيذ + تحقّق + ذكاء اصطناعي + ذكاء اصطناعي فيزيائي + إنترنت الأشياء
```

---

## الصيغة التي كان الجميع ينتظرها

لا توجد صيغة حالية تجمع الخصائص الخمس معًا:

|            | قابلة للقراءة البشرية | قابلة للتنفيذ | أصلية للذكاء الاصطناعي | ذاتية التحقّق | ذكاء اصطناعي فيزيائي |
| ---------- | --------------------- | ------------- | ---------------------- | ------------- | -------------------- |
| Markdown   | ✅                     | ❌             | ❌                      | ❌             | ❌                    |
| Jupyter    | ❌ (JSON)              | ✅             | ❌                      | ❌             | ❌                    |
| AGENTS.md  | ✅                     | ❌             | ✅                      | ❌             | ❌                    |
| Terraform  | ❌                     | ✅             | ❌                      | △             | ❌                    |
| Ansible    | ❌ (YAML)              | ✅             | △                      | ❌             | ❌                    |
| RUNME      | ✅                     | ✅             | ❌                      | ❌             | ❌                    |
| **`.wia`** | **✅**                 | **✅**         | **✅**                  | **✅**         | **✅**                |

---

## أكثر من 45 صيغة تتحوّل إلى .wia

`.wia` هي **المجموعة الشاملة** —— كل ما يلي يمكن تحويله إليها:

**المستندات والإعدادات**: `.md` · `.txt` · `.rst` · `.adoc` · `.json` · `.yml` · `.toml` · `.ini` · `.xml` · `.env` · `.properties` · `.plist` · `.csv` · `.log`

**البرمجة**: `.sh` · `.py` · `.sql` · `.js` · `.ts` · `.go` · `.rs` · `.rb` · `.java` · `.c` · `.cpp` · `.lua` · `.ps1`

**البنية التحتية**: `.tf` · `.hcl` · `Dockerfile` · `docker-compose.yml` · `Jenkinsfile` · `.gradle` · `Vagrantfile` · `Makefile` · `crontab` · `nginx.conf`

**واجهات البرمجة والمخططات**: `.proto` · `.graphql` · `.prisma`

**علم البيانات**: `.ipynb` (تحويل Jupyter → كتل .wia)

**إمكانية الوصول**: `.brf` · `.brl` (برايل)

---

## الميزات

### أنواع الكتل
`sh run` · `sql run on=` · `ai [model=]` · `verify expect=` · `python run` · `node run` · `display`

### خصائص الكتل
`run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` · `pipe` · `retry=` · `converge=` · `drift=`

### أنواع الإدخال
`string` · `number` · `boolean` · `enum` · `secret` · `file` · `array`

### المتغيرات الخاصة
`{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` · `{{$os}}` · `{{$arch}}`

### الأمان
بوابات الموافقة · وضع التشغيل التجريبي · التراجع (`on_fail=`) · الخمول (idempotency) · إخفاء الأسرار · منع حقن الأوامر (shell injection)

### تكامل الذكاء الاصطناعي
وكيل Soomy التلقائي · اختيار النموذج · صور الرؤية · تحليل النتائج بالذكاء الاصطناعي · توليد `.wia` بالذكاء الاصطناعي («اصنع لي runbook»)

### الامتثال
سجل التنفيذ (مسار تدقيق) · تصدير تقارير HTML · توليد أدلة SOC 2 / ISO 27001 / ISO 9001 (**22 ضابطًا آليًا** —— 9 لـ SOC 2، و8 لـ ISO 27001، و5 لـ ISO 9001)

---

## مكتوبة بأي لغة من 254 لغة

ملف `.wia` هو نص UTF-8 عادي. يكتب المؤلف بلغته الخاصة —— وينفّذ وقت التشغيل بالطريقة نفسها بصرف النظر عن اللغة البشرية للنص.

هذا ليس مجرد ادعاء؛ بل موجود في الأمثلة. فمثلًا، الملف [`examples/server-health.wia`](examples/server-health.wia) مكتوب بالكورية (`title: WIA SOOM 서버 건강 점검`) ويعمل تمامًا مثل أي runbook بالإنجليزية. يستطيع أي مشغّل ميداني بأي لغة من **254 لغة** أن يقرأ ويكتب وينفّذ `.wia` بلغته الأم، كما أن واجهة وقت التشغيل **WIA SOOM** مترجمة إلى الـ254 لغة جميعها.

إمكانية الوصول مدمجة بالروح نفسها: WCAG AA، والنصوص من اليمين إلى اليسار (RTL)، وبرايل (`.brf` / `.brl`)، والتنقل الكامل عبر لوحة المفاتيح. الهدف هو صيغة تشغيلية واحدة يستطيع قراءتها المحكمة والمدقّق والروبوت والمشغّل الكفيف بلغته الأم.

---

## الذكاء الاصطناعي الفيزيائي وROS 2 وإنترنت الأشياء

`.wia` مبنية من أجل **عمليات أساطيل الروبوتات** و**إدارة أجهزة إنترنت الأشياء**:

### إدارة روبوتات ROS 2
- جسر ROS 2 CLI قائم على SSH (**27 نقطة اتصال IPC**)
- مراقبة صحة الروبوت (العقد، المواضيع، الخدمات، البطارية، حرارة المعالج)
- تشخيص الروبوتات بالذكاء الاصطناعي
- تسجيل / إعادة تشغيل / تحليل ros2 bag
- محرّك التقارب نحو الحالة المطلوبة + كشف انحراف الإعدادات (على مستوى الأسطول)
- توليد تلقائي لـ runbooks الاستعادة بصيغة `.wia`

### إدارة أجهزة إنترنت الأشياء
أي جهاز يعمل بنظام Linux مع SSH = جاهز لـ `.wia`: راسبيري باي · مستشعرات المصانع الذكية · المزارع الذكية · CCTV/NVR · معدات الشبكات · الطائرات المسيّرة · المركبات ذاتية القيادة.

### البرمجيات مقابل العتاد
تحل `.wia` عن بُعد **مشكلات البرمجيات** (غالبية «الأعطال» التشغيلية) —— تعطّل العمليات (إعادة التشغيل)، ومشكلات الذاكرة (التنظيف)، وأخطاء الإعداد (الاستعادة)، وانقطاع الشبكة (إعادة الاتصال) —— دون زيارة ميدانية. أما أعطال العتاد (تلف المحرّك أو المستشعر) فتتطلب أيدي بشرية، لكن `.wia` تظل تساعد في التشخيص والوقاية والتحقق بعد الإصلاح.

---

## 111 runbook نموذجيًا

يحتوي مجلد [`examples/`](examples) على **111 runbook جاهزًا للإنتاج** (عدد مُتحقَّق منه) ضمن 13 فئة:

| الفئة | العدد | أمثلة |
| ----- | ----- | ----- |
| 🖥️ الخادم / نظام التشغيل | 13 | `amazon-linux-setup.wia`، `ssh-hardening.wia`، `linux-performance-tuning.wia` |
| 🌐 الويب / التطبيقات | 10 | `nginx-install.wia`، `wordpress-install.wia`، `nodejs-deploy.wia`، `pm2-deploy.wia` |
| 🗄️ قواعد البيانات | 10 | `mysql-install.wia`، `postgresql-backup.wia`، `redis-install.wia`، `mongodb-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`، `docker-compose-deploy.wia`، `docker-registry.wia` |
| ☸️ Kubernetes | 9 | `k8s-cluster-check.wia`، `k8s-rollback.wia`، `helm-install-app.wia` |
| 📊 المراقبة / السجلات | 9 | `prometheus-install.wia`، `elk-stack-setup.wia`، `log-investigation.wia` |
| 🔒 الأمان / الامتثال | 13 | `security-audit.wia`، `fail2ban-setup.wia`، `ssl-cert-renewal.wia`، `aws-iam-audit.wia` |
| 🔄 CI/CD / IaC | 6 | `github-actions-setup.wia`، `terraform-apply.wia`، `ansible-playbook-run.wia` |
| ☁️ السحابة / AWS | 8 | `aws-cli-setup.wia`، `s3-backup.wia`، `ec2-snapshot.wia`، `autoscaling-setup.wia` |
| 🌍 الشبكة / DNS | 6 | `network-troubleshoot.wia`، `dns-troubleshoot.wia`، `site-failover-dns.wia` |
| 📧 الاتصالات | 3 | `postfix-setup.wia`، `smtp-test.wia`، `slack-webhook.wia` |
| 🤖 الروبوت / ROS 2 | 10 | `ros-diagnostic.wia`، `ros-node-recovery.wia`، `robot-fleet-health.wia`، `ros2-bag-record.wia` |
| 🏥 الحوادث / التعافي من الكوارث | 10 | `high-cpu-response.wia`، `oom-response.wia`، `disk-full-response.wia`، `disaster-recovery-plan.wia` |

---

## المنظومة

| الأداة | الدور | الحالة |
| ------ | ----- | ------ |
| **[WIA SOOM](https://wiasoom.com)** | وقت التشغيل المرجعي (Win/Mac/Linux) | ✅ v3.9.29 |
| **[Spec v1](SPEC-v1.md)** | المواصفة الرسمية (19 قسمًا) | ✅ منشورة |
| **[111 runbook](examples)** | قوالب جاهزة للإنتاج | ✅ متاحة |
| **[الورقة (Zenodo)](https://doi.org/10.5281/zenodo.20448006)** | مسودة قابلة للاستشهاد + DOI (CC-BY 4.0) | ✅ منشورة |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | صفحة تعريف الصيغة | ✅ مباشرة |
| **[المحوّل](https://wia.wiasoom.com/convert.html)** | أكثر من 45 صيغة → .wia | ✅ مباشر |
| **[العارض](https://wia.wiasoom.com/view.html)** | قراءة .wia دون تثبيت | ✅ مباشر |
| **Rust CLI** (`wia`) | محوّل/منفّذ بملف ثنائي واحد | 🔜 خارطة الطريق |
| **امتداد VS Code** | تمييز بناء الجملة + معاينة | 🔜 خارطة الطريق |

### خارطة طريق أدوات Rust

```
libwia (مكتبة Rust الأساسية)
├── wia CLI      → محوّل/منفّذ بملف ثنائي واحد
├── وحدة WASM    → أدوات المتصفح بسرعة أصلية
└── napi-rs      → تكامل مع تطبيق Electron
```

---

## مبادئ التصميم

1. **مجموعة شاملة من Markdown** —— كل `.md` هو `.wia` صالح
2. **الإنسان أولًا** —— قابل للقراءة دون أي أداة
3. **لا تنفيذ تلقائي** —— على المستخدم النقر على Run (الأمان)
4. **مستقل عن اللغة** —— 254 لغة بشرية، وأي لغة برمجة
5. **قابل للنقل** —— نص عادي، دون احتكار من مورّد
6. **ذاتي التحقّق** —— تأكيدات مدمجة
7. **أصلي للذكاء الاصطناعي** —— يستطيع الذكاء الاصطناعي القراءة والتنفيذ والتوسيع والتحقّق
8. **جاهز للذكاء الاصطناعي الفيزيائي** —— عمليات أسطول ROS 2 + إنترنت الأشياء
9. **متاح للجميع** —— WCAG AA، RTL، برايل، التنقل عبر لوحة المفاتيح

## الاستشهاد

إذا أشرت إلى `.wia` في عمل أكاديمي أو تقني، يُرجى الاستشهاد بالمسودة:

> Yeon, Sam-heum. *.wia: An AI-Native Document Format for Executable, Self-Verifying Operations in Physical AI.* Zenodo, 2026. https://doi.org/10.5281/zenodo.20448006

## نوع MIME

`text/vnd.wia`

## الترخيص

المواصفة: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · الأمثلة: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

من إنشاء **[Smilestory Co., Ltd.](https://smilestory.net)** (WIA Standards) · [wiasoom.com](https://wiasoom.com)

</div>
