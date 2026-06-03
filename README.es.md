# `.wia` — El formato de documento nativo de IA

**Idioma:** [English](README.md) · [한국어](README.ko.md) · [中文](README.zh.md) · [日本語](README.ja.md) · Español · [العربية](README.ar.md)

> **Los humanos escriben. La IA ejecuta. Las máquinas verifican. Los robots convergen.**

`.wia` es un superconjunto de Markdown. Todo `.md` es un `.wia` válido.
Lo que Markdown no puede hacer, `.wia` lo añade —— y nada más.

```
Markdown  = leer
.wia      = leer + ejecutar + verificar + IA + IA física + IoT
```

---

## El formato que todos esperaban

Ningún formato existente combina los cinco:

|            | Legible por humanos | Ejecutable | Nativo de IA | Autoverificable | IA física |
| ---------- | ------------------- | ---------- | ------------ | --------------- | --------- |
| Markdown   | ✅                   | ❌          | ❌            | ❌               | ❌         |
| Jupyter    | ❌ (JSON)            | ✅          | ❌            | ❌               | ❌         |
| AGENTS.md  | ✅                   | ❌          | ✅            | ❌               | ❌         |
| Terraform  | ❌                   | ✅          | ❌            | △               | ❌         |
| Ansible    | ❌ (YAML)            | ✅          | △            | ❌               | ❌         |
| RUNME      | ✅                   | ✅          | ❌            | ❌               | ❌         |
| **`.wia`** | **✅**               | **✅**      | **✅**        | **✅**           | **✅**     |

---

## Más de 45 formatos se convierten a .wia

`.wia` es el **superconjunto** —— todo lo siguiente puede convertirse hacia arriba:

**Documentos y configuración**: `.md` · `.txt` · `.rst` · `.adoc` · `.json` · `.yml` · `.toml` · `.ini` · `.xml` · `.env` · `.properties` · `.plist` · `.csv` · `.log`

**Programación**: `.sh` · `.py` · `.sql` · `.js` · `.ts` · `.go` · `.rs` · `.rb` · `.java` · `.c` · `.cpp` · `.lua` · `.ps1`

**Infraestructura**: `.tf` · `.hcl` · `Dockerfile` · `docker-compose.yml` · `Jenkinsfile` · `.gradle` · `Vagrantfile` · `Makefile` · `crontab` · `nginx.conf`

**API y esquemas**: `.proto` · `.graphql` · `.prisma`

**Ciencia de datos**: `.ipynb` (conversión Jupyter → bloques .wia)

**Accesibilidad**: `.brf` · `.brl` (Braille)

---

## Características

### Tipos de bloque
`sh run` · `sql run on=` · `ai [model=]` · `verify expect=` · `python run` · `node run` · `display`

### Atributos de bloque
`run` · `on=` · `expect=` · `model=` · `timeout=` · `if=` · `watch=` · `approve` · `on_fail=` · `idempotent` · `pipe` · `retry=` · `converge=` · `drift=`

### Tipos de entrada
`string` · `number` · `boolean` · `enum` · `secret` · `file` · `array`

### Variables especiales
`{{$prev}}` · `{{$timestamp}}` · `{{$hostname}}` · `{{$user}}` · `{{$os}}` · `{{$arch}}`

### Seguridad
Puertas de aprobación · Modo de simulación · Reversión (`on_fail=`) · Idempotencia · Enmascaramiento de secretos · Prevención de inyección de shell

### Integración de IA
Agente automático Soomy · Selección de modelo · Imágenes de visión · Análisis de resultados con IA · Generación de .wia con IA («hazme un runbook»)

### Cumplimiento
Registro de ejecución (rastro de auditoría) · Exportación de informes HTML · Generación de evidencia SOC 2 / ISO 27001 / ISO 9001 (**22 controles automatizados** —— 9 SOC 2, 8 ISO 27001, 5 ISO 9001)

---

## Escrito en cualquiera de 254 idiomas

Un `.wia` es texto UTF-8 plano. El autor escribe en su propio idioma —— el runtime ejecuta de forma idéntica sin importar el idioma humano de la prosa.

Esto no es una afirmación; está en los ejemplos. Por ejemplo, [`examples/server-health.wia`](examples/server-health.wia) está escrito en coreano (`title: WIA SOOM 서버 건강 점검`) y se ejecuta exactamente igual que un runbook en inglés. Un operador de campo en cualquiera de **254 idiomas** puede leer, escribir y ejecutar `.wia` en su lengua materna, y la interfaz del runtime **WIA SOOM** está localizada a los 254.

La accesibilidad está integrada con el mismo espíritu: WCAG AA, escrituras RTL, Braille (`.brf` / `.brl`) y navegación completa por teclado. El objetivo es un único formato operativo que un tribunal, un auditor, un robot y un operador ciego en su idioma nativo puedan leer todos.

---

## IA física, ROS 2 e IoT

`.wia` está construido para **operaciones de flotas de robots** y **gestión de dispositivos IoT**:

### Gestión de robots ROS 2
- Puente CLI ROS 2 basado en SSH (**27 puntos de conexión IPC**)
- Monitoreo de salud del robot (nodos, tópicos, servicios, batería, temperatura de CPU)
- Diagnóstico de robots con IA
- Grabación / reproducción / análisis de ros2 bag
- Motor de convergencia al estado deseado + detección de deriva de configuración (toda la flota)
- Runbooks de recuperación `.wia` autogenerados

### Gestión de dispositivos IoT
Cualquier dispositivo con Linux y SSH = listo para `.wia`: Raspberry Pi · sensores de fábrica inteligente · granja inteligente · CCTV/NVR · equipos de red · drones · vehículos autónomos.

### Software vs. hardware
`.wia` resuelve de forma remota los **problemas de software** (la mayoría de los «fallos» operativos) —— caídas de procesos (reinicio), problemas de memoria (limpieza), errores de configuración (restauración), caídas de red (reconexión) —— sin visita presencial. Los fallos de hardware (motor, daño de sensor) requieren manos humanas, pero `.wia` aún ayuda con el diagnóstico, la prevención y la verificación posterior a la reparación.

---

## 111 runbooks de ejemplo

El directorio [`examples/`](examples) contiene **111 runbooks listos para producción** (recuento verificado) en 13 categorías:

| Categoría | Cantidad | Ejemplos |
| --------- | -------- | -------- |
| 🖥️ Servidor / SO | 13 | `amazon-linux-setup.wia`, `ssh-hardening.wia`, `linux-performance-tuning.wia` |
| 🌐 Web / Aplicación | 10 | `nginx-install.wia`, `wordpress-install.wia`, `nodejs-deploy.wia`, `pm2-deploy.wia` |
| 🗄️ Base de datos | 10 | `mysql-install.wia`, `postgresql-backup.wia`, `redis-install.wia`, `mongodb-install.wia` |
| 🐳 Docker | 4 | `docker-install.wia`, `docker-compose-deploy.wia`, `docker-registry.wia` |
| ☸️ Kubernetes | 9 | `k8s-cluster-check.wia`, `k8s-rollback.wia`, `helm-install-app.wia` |
| 📊 Monitoreo / Registros | 9 | `prometheus-install.wia`, `elk-stack-setup.wia`, `log-investigation.wia` |
| 🔒 Seguridad / Cumplimiento | 13 | `security-audit.wia`, `fail2ban-setup.wia`, `ssl-cert-renewal.wia`, `aws-iam-audit.wia` |
| 🔄 CI/CD / IaC | 6 | `github-actions-setup.wia`, `terraform-apply.wia`, `ansible-playbook-run.wia` |
| ☁️ Nube / AWS | 8 | `aws-cli-setup.wia`, `s3-backup.wia`, `ec2-snapshot.wia`, `autoscaling-setup.wia` |
| 🌍 Red / DNS | 6 | `network-troubleshoot.wia`, `dns-troubleshoot.wia`, `site-failover-dns.wia` |
| 📧 Comunicación | 3 | `postfix-setup.wia`, `smtp-test.wia`, `slack-webhook.wia` |
| 🤖 Robot / ROS 2 | 10 | `ros-diagnostic.wia`, `ros-node-recovery.wia`, `robot-fleet-health.wia`, `ros2-bag-record.wia` |
| 🏥 Incidentes / DR | 10 | `high-cpu-response.wia`, `oom-response.wia`, `disk-full-response.wia`, `disaster-recovery-plan.wia` |

---

## Ecosistema

| Herramienta | Rol | Estado |
| ----------- | --- | ------ |
| **[WIA SOOM](https://wiasoom.com)** | Runtime de referencia (Win/Mac/Linux) | ✅ v3.9.29 |
| **[Spec v1](SPEC-v1.md)** | Especificación formal (19 secciones) | ✅ Publicado |
| **[111 runbooks](examples)** | Plantillas listas para producción | ✅ Disponible |
| **[Artículo (Zenodo)](https://doi.org/10.5281/zenodo.20448006)** | Preprint citable + DOI (CC-BY 4.0) | ✅ Publicado |
| **[wia.wiasoom.com](https://wia.wiasoom.com)** | Página del formato | ✅ En línea |
| **[Conversor](https://wia.wiasoom.com/convert.html)** | 45+ formatos → .wia | ✅ En línea |
| **[Visor](https://wia.wiasoom.com/view.html)** | Leer .wia sin instalar | ✅ En línea |
| **Rust CLI** (`wia`) | Convertidor/ejecutor de binario único | 🔜 Hoja de ruta |
| **Extensión de VS Code** | Resaltado de sintaxis + vista previa | 🔜 Hoja de ruta |

### Hoja de ruta de herramientas Rust

```
libwia (biblioteca central en Rust)
├── wia CLI      → convertidor/ejecutor de binario único
├── módulo WASM  → herramientas de navegador a velocidad nativa
└── napi-rs      → integración con la app Electron
```

---

## Principios de diseño

1. **Superconjunto de Markdown** —— todo `.md` es un `.wia` válido
2. **Humano primero** —— legible sin ninguna herramienta
3. **Sin ejecución automática** —— el usuario debe pulsar Run (seguridad)
4. **Independiente del idioma** —— 254 idiomas humanos, cualquier lenguaje de programación
5. **Portable** —— texto plano, sin dependencia de proveedor
6. **Autoverificable** —— aserciones integradas
7. **Nativo de IA** —— la IA puede leer, ejecutar, ampliar y verificar
8. **Listo para IA física** —— operaciones de flota ROS 2 + IoT
9. **Accesible** —— WCAG AA, RTL, Braille, navegación por teclado

## Cita

Si haces referencia a `.wia` en un trabajo académico o técnico, por favor cita el preprint:

> Yeon, Sam-heum. *.wia: An AI-Native Document Format for Executable, Self-Verifying Operations in Physical AI.* Zenodo, 2026. https://doi.org/10.5281/zenodo.20448006

## Tipo MIME

`text/vnd.wia`

## Licencia

Especificación: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) · Ejemplos: [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)

---

Creado por **[Smilestory Co., Ltd.](https://smilestory.net)** (WIA Standards) · [wiasoom.com](https://wiasoom.com)
