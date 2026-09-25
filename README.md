# 💰 EZBookKeeping Docker - Personal Finance Autohospedado

[![GitHub Stars](https://img.shields.io/github/stars/mayswind/ezbookkeeping?style=flat-square&logo=github)](https://github.com/mayswind/ezbookkeeping)
[![Docker Pulls](https://img.shields.io/docker/pulls/mayswind/ezbookkeeping?style=flat-square&logo=docker)](https://hub.docker.com/r/mayswind/ezbookkeeping)
[![License](https://img.shields.io/github/license/mayswind/ezbookkeeping?style=flat-square)](https://github.com/mayswind/ezbookkeeping/blob/master/LICENSE)
[![Docker Image Version](https://img.shields.io/docker/v/mayswind/ezbookkeeping/latest?style=flat-square&logo=docker)](https://hub.docker.com/r/mayswind/ezbookkeeping/tags)

## 📋 Descripción general

**EZBookKeeping** es una aplicación de finanzas personales completamente autohospedada, *lightweight* y fácil de usar construida con **Go (backend)** + **React (frontend)**. Proporciona registro de transacciones diarias, importación de datos en múltiples formatos (CSV, OFX, QFX, QIF, IIF), búsqueda y filtrado avanzado, gráficas integradas para análisis, soporte **PWA (Progressive Web App)**, interfaces adaptadas mobile/desktop, soporte **multi-database** (SQLite, MySQL, PostgreSQL), funciona perfectamente en Raspberry Pi, NAS, MicroServers, arquitectura multi-plataforma (amd64, arm64, armv7), presupuestos y categorías personalizadas, exportación de datos, sin publicidades, completamente privado.

> 🎯 **Propuesta clave**: Lightweight personal finance app (Go + React) • 3.5k+ GitHub stars • MIT open source • Production-ready

## ✨ Características principales

- 📝 **Registro transacciones** — Registro diario fácil, categorías custom, múltiples cuentas, balance tracking
- 📥 **Import datos** — CSV, OFX, QFX, QIF, IIF • Batch import • Mapeo automático • Data validation
- 🔍 **Search + filter** — Búsqueda avanzada • Filtros por fecha, categoría, monto • Full-text search
- 📊 **Built-in charts** — Gráficas automáticas • Spending trends • Income analysis • Custom dimensions
- 📱 **PWA support** — Progressive Web App • Add to home screen mobile • Offline capability
- 💻 **Mobile optimized** — Responsive UI • Touch-friendly • Mobile-first design • Desktop adaption
- 💰 **Budget management** — Set budgets por categoría • Track vs budget • Alerts cuando se excede
- 🗄️ **Multi-database** — SQLite, MySQL, PostgreSQL • Choose backend • Easy migration
- 📤 **Data export** — Export a CSV • Backup datos • Migrate fácilmente • No vendor lock-in
- 👥 **User management** — Multiple users • Separate finances • Admin panel • User roles
- 🏷️ **Custom categories** — Create categorías custom • Organize gasto • Flexible taxonomy
- ⚡ **Low resource** — Runs on Raspberry Pi • NAS compatible • Minimal CPU/RAM usage

## 📋 Requisitos del sistema

- **Docker & Docker Compose v2+**
- **RAM**: 256 MB - 1 GB mínimo (ultra-ligero)
- **Disco**: 100 MB - 50GB+ espacio disco (según datos transacciones)
- **Puerto TCP**: 8080 (web UI, configurable)
- **Database**: SQLite (embedded, default) **O** MySQL/PostgreSQL (external)
- **Arquitectura**: multi-arch (amd64, arm64, armv7, i386)
- **OS**: Linux, Windows, macOS (compatible)
- **Opcional**: Reverse proxy nginx/Caddy para HTTPS

> 💡 **Muy ligero**: Ideal para Raspberry Pi, NAS, VPS económicos. Bajo consumo CPU/RAM.

## 🐳 Instalación

### Paso 1: docker-compose.yml (simple con SQLite)

```yaml
version: '3.8'

services:
  ezbookkeeping:
    image: mayswind/ezbookkeeping:latest
    container_name: ezbookkeeping
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - ./data:/data
    environment:
      - TZ=America/Mexico_City
      # SQLite database incrustado en ./data/ezbookkeeping.db
```

### Paso 2: Iniciar EZBookKeeping

```bash
docker compose up -d
# Espera ~10 segundos para que inicie
docker compose logs -f
```

### Paso 3: Acceder a EZBookKeeping

```bash
# Abre en navegador:
http://localhost:8080

# Desde otro dispositivo:
http://192.168.1.100:8080
```

| Componente | URL / Ruta |
|------------|------------|
| 💰 EZBookKeeping Web UI | `http://localhost:8080` |
| 📊 Carpeta datos | `./data` (SQLite database + config) |

## ⚙️ Configuración

1. **Zona horaria** — Ajusta `TZ` en `environment` (ej: `Europe/Madrid`, `America/Mexico_City`)
2. **Puerto host** — Cambia `"8080:8080"` a `"<puerto_host>:8080"` si 8080 está ocupado
3. **Persistencia** — El volumen `./data:/data` guarda SQLite DB + configuración
4. **Base de datos externa** — Ver sección *Configuración avanzada* para PostgreSQL/MySQL
5. **Reverse proxy** — Configura nginx/Caddy apuntando a `http://ezbookkeeping:8080` para HTTPS

## 🚀 Primeros pasos

1. Abre `http://localhost:8080` en navegador
2. Interfaz web limpia y responsiva carga
3. Crea cuenta de usuario + contraseña (primera ejecución = setup inicial)
4. Login con credenciales creadas
5. Dashboard aparece con overview finanzas
6. Start recording transacciones o importa datos CSV
7. Crea categorías custom para organizar gasto
8. View gráficas automáticas de spending patterns

> 💡 **Sin login predeterminado**: Primera ejecución requiere setup inicial. Crea usuario admin.

## 💡 Casos de uso

- **Personal finance tracking** — Record daily transactions • Analyze spending • Budget management
- **Household expenses** — Family finance shared • Multiple user accounts • Separate tracking
- **Small business accounting** — Invoice tracking • Expense records • Simple bookkeeping
- **Data import** — Import banking CSV/OFX • Automatic categorization • Deduplication
- **Analytics** — Spending trends • Income vs expenses • Custom charts dimensions
- **Privacy-focused** — Self-hosted • No ads • Complete data control • Export anytime
- **Low-resource deployment** — Raspberry Pi, NAS, VPS económicos • Minimal requirements

## 🔒 Acceso remoto seguro

Para exponer EZBookKeeping de forma segura a Internet:

1. **Reverse Proxy** (nginx/Caddy/Traefik) con terminación SSL
2. **Autenticación adicional** — Basic Auth, Authelia, oAuth2-Proxy
3. **VPN** — WireGuard, Tailscale, OpenVPN (recomendado para máxima privacidad)
4. **Cloudflare Tunnel** — Sin abrir puertos en router
5. **Firewall** — Restringe acceso a IPs de confianza si no usas VPN

> ⚠️ **Nunca expongas el puerto 8080 directamente a Internet** sin autenticación y TLS.

## 🛠️ Gestión y mantenimiento

### Ver estado
```bash
docker compose ps
```

### Ver logs
```bash
docker compose logs -f ezbookkeeping
```

### Detener EZBookKeeping
```bash
docker compose down
```

### Actualizar versión
```bash
docker compose pull
docker compose up -d
# Datos persistentes se mantienen en ./data
```

### Backup de datos
```bash
# Opción 1: Backup comprimido desde contenedor
docker compose exec ezbookkeeping tar -czf /data/backup-$(date +%Y%m%d).tar.gz /data

# Opción 2: Backup carpeta host (recomendado)
cp -r data data_backup_$(date +%Y%m%d)
```

### Monitorear consumo
```bash
docker stats ezbookkeeping
# Típicamente:
# CPU: < 1%
# RAM: 50-200MB (muy ligero)
# Pico durante import: ~300MB
```

## 📝 Licencia

**MIT License** — Código abierto, uso comercial permitido, sin garantía.

- Repositorio oficial: [mayswind/ezbookkeeping](https://github.com/mayswind/ezbookkeeping)
- Licencia: [LICENSE](https://github.com/mayswind/ezbookkeeping/blob/master/LICENSE)

---

> 📖 **Artículo original**: [Cómo instalar EZBookKeeping en Docker - Personal Finance autohospedado](https://genbyte.blogspot.com/2026/09/como-instalar-ezbookkeeping-en-docker.html)  
> 🎥 **Vídeo tutorial**: [Canal GENBYTE YouTube](https://www.youtube.com/@genbyte)  
> 🐳 **Docker Hub**: [mayswind/ezbookkeeping](https://hub.docker.com/r/mayswind/ezbookkeeping)  
> 🌐 **Live Demo**: [demo.ezbookkeeping.com](https://demo.ezbookkeeping.com)