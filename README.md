# TeleCorp — Sistema de Gestión de Telefonía Móvil

> Sistema interno de gestión de telefonía móvil corporativa desarrollado para Cencosud Argentina.

---

## ¿Qué es TeleCorp?

TeleCorp es una plataforma web que centraliza y digitaliza la operación completa de telefonía móvil de Cencosud. Reemplaza un proceso manual basado en múltiples archivos Excel que generaba inconsistencias, historial desactualizado y errores operativos frecuentes.

Con TeleCorp, toda la operación — desde el alta de una línea hasta la baja del empleado y la devolución del equipo — se gestiona en un único sistema con trazabilidad completa.

---

## Stack tecnológico

| Capa | Tecnología |
|---|---|
| Backend | Python 3 + Flask + Waitress |
| Base de datos | SQL Server (pyodbc) |
| Proxy | NGINX |
| Frontend | HTML / CSS / JavaScript (vanilla) |
| Autenticación | Active Directory corporativo (LDAP) |
| Servidor actual | Windows — PC host interna |

---

## Estructura del proyecto

```
TELECORP/
│
├── app.py                  # Backend Flask — 40+ endpoints REST
├── index.html              # Aplicación principal (todos los módulos)
├── login.html              # Página de autenticación
├── run_produccion.py       # Levanta Flask con Waitress en modo producción
├── mantenimiento_telecorp.bat   # Mantenimiento semanal automatizado (domingos 02:00hs)
├── reiniciar_telecorp.bat       # Reinicio rápido del sistema
└── logs/                   # Logs de mantenimiento (generados automáticamente)
```

---

## Módulos del sistema

- **Dashboard** — KPIs en tiempo real: líneas activas, gestiones del día, stock disponible
- **Líneas** — Alta, baja, modificación y búsqueda de líneas celulares
- **Historial de gestiones** — Registro completo de todas las solicitudes con estados y auditoría
- **Bajas y devoluciones** — Procesamiento masivo de bajas desde CSV de RRHH, gestión de equipos
- **Stock disponible** — Control de equipos recuperados listos para reasignar
- **Lista de precios** — Equipos disponibles por gama (A/B/C/D) con actualización semanal
- **Maestro RRHH** — Nómina de empleados con actualización mensual
- **Auditoría** — Log completo de todas las acciones del sistema
- **Despacho** — Gestión de envíos AMBA e Interior
- **Makro** — Módulo independiente para la cadena Makro

---

## Cómo correr el proyecto

### Requisitos
- Python 3.10+
- SQL Server con la base de datos `TelefoniaDB`
- NGINX instalado en `C:\nginx`
- Active Directory de Cencosud accesible (para autenticación)

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/Thom1074/TELECORP.git
cd TELECORP

# Crear entorno virtual
python -m venv .venv
.venv\Scripts\activate

# Instalar dependencias
pip install flask waitress pyodbc python-ldap
```

### Levantar en producción

```bash
# Activar entorno virtual
.venv\Scripts\activate

# Iniciar NGINX
cd C:\nginx && nginx.exe

# Iniciar TeleCorp
cd C:\ruta\al\proyecto
py run_produccion.py
```

O simplemente ejecutar `reiniciar_telecorp.bat` como Administrador.

### Acceso
```
http://G100603NT427        # Red interna Cencosud Argentina
Usuario: usuario.de.red
Contraseña: contraseña corporativa
```

---

## Roles

| Rol | Permisos |
|---|---|
| `admin` | Acceso total a todos los módulos — puede crear, editar y eliminar |
| `consulta` | Solo lectura — puede ver datos pero no modificar |

---

## Estado del proyecto

### ✅ Etapa 1 — En producción (Argentina)
- Gestión completa de líneas y equipos
- Historial con trazabilidad completa
- Procesamiento de bajas desde CSV de RRHH
- Dashboard operativo con KPIs en tiempo real
- Stock disponible y reasignación de equipos
- Auditoría de todas las acciones
- Autenticación corporativa (Active Directory)
- Mantenimiento y backup semanal automatizado

### 🔄 Etapa 2 — En planificación
- Módulo de facturación — conciliación de facturas vs. líneas activas
- Integración con Makro — unificación en la misma plataforma
- Migración a servidor corporativo — infraestructura IT con alta disponibilidad
- Reportes en Power BI — dashboards ejecutivos por área y período
- Aplicación de escritorio — ejecutable instalable para acceso directo desde Windows

---

## Cobertura regional

| País | Estado |
|---|---|
| 🇦🇷 Argentina | ✅ En producción |
| 🇨🇱 Chile | 🔄 Planificado |
| 🇧🇷 Brasil | 🔄 Planificado |
| 🇵🇪 Perú | 🔄 Planificado |
| 🇨🇴 Colombia | 🔄 Planificado |

---

## Base de datos

**SQL Server — `TelefoniaDB`**

| Tabla | Contenido |
|---|---|
| `dbo.Lineas` | Líneas celulares activas y su historial |
| `dbo.Gestiones` | Todas las solicitudes y gestiones de equipos |
| `dbo.Maestro` | Nómina de empleados (carga mensual) |
| `dbo.Precios` | Lista de equipos disponibles por gama |
| `dbo.Auditoria` | Log de todas las acciones del sistema |
| `dbo.Usuarios` | Usuarios del sistema con roles |

---

## Autor

**Thomas Salinas Litardo**  
Telefonía Empresarial — Cencosud Argentina  
Área de Sistemas y Operaciones

---

*Desarrollado internamente por el área de Telefonía Empresarial de Cencosud Argentina.*
