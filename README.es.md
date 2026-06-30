# NetGuard Pro

[🇧🇷 Português](./README.md) | [🇬🇧 English](./README.en.md)

Gestión y seguridad de redes en tiempo real: supervise, proteja y optimice su infraestructura desde un único panel.

NetGuard Pro supervisa continuamente el rendimiento de sus servidores (CPU, memoria, disco, latencia y pérdida de paquetes), activa la conmutación por error automática cuando ocurre una falla y protege su red con un firewall configurable y detección de amenazas.

---

## Índice

- [Primeros Pasos](#primeros-pasos)
- [Características Principales](#características-principales)
- [Caso de Uso: Reducción del Tiempo de Inactividad con Failover](#caso-de-uso-reducción-del-tiempo-de-inactividad-con-failover)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Para Desarrolladores: Integración mediante API](#para-desarrolladores-integración-mediante-api)
- [Cómo Contribuir](#cómo-contribuir)
- [Solución de Problemas](#solución-de-problemas)
- [Soporte](#soporte)
- [Licencia](#licencia)

---

## Primeros Pasos

### Requisitos

- Ubuntu Linux 20.04+ o Windows Server 2019+
- 8 GB de RAM (16 GB recomendados para producción)
- Docker instalado
- Acceso saliente por el puerto 443

### Instalación

```bash
git clone https://github.com/netguardpro/netguard-pro.git
cd netguard-pro
docker compose up -d
```

### Primer Acceso

1. Abra `http://localhost:8080` en su navegador.
2. Cree una cuenta de administrador.
3. Agregue el primer servidor que desea supervisar (IP + credenciales).
4. ¡Listo! En pocos segundos las métricas comenzarán a aparecer en el panel.

> **Consejo:** Empiece supervisando solo 1 o 2 servidores críticos antes de añadir toda su infraestructura. Esto facilita validar las alertas y las reglas del firewall sin generar ruido innecesario.

---

## Características Principales

| Característica | Descripción |
| --- | --- |
| **Monitoreo en tiempo real** | Supervisa CPU, memoria, disco, latencia y pérdida de paquetes |
| **Failover automático** | Redirige el tráfico a un servicio de respaldo cuando falla el principal |
| **Balanceo de carga** | Distribuye las solicitudes entre los servidores para evitar sobrecargas |
| **Firewall configurable** | Define reglas de acceso por IP, puerto o servicio |
| **Detección de amenazas** | Identifica actividades sospechosas con alertas priorizadas |
| **Panel personalizable** | Permite que cada equipo elija las métricas destacadas |

---

## Caso de Uso: Reducción del Tiempo de Inactividad con Failover

**Escenario:** Un equipo de TI mantiene un servicio crítico de autenticación en un único servidor. Durante un pico de tráfico, el servidor principal comienza a fallar.

**Con NetGuard Pro:**

1. El sistema detecta la degradación del rendimiento mediante monitoreo continuo.
2. El failover automático redirige las solicitudes al servidor de respaldo en cuestión de segundos.
3. Se envía una alerta al equipo con el historial de métricas que originó la transición.
4. El equipo confirma desde el panel que el servicio se ha estabilizado sin necesidad de intervenir manualmente.

**Resultado:** El tiempo de inactividad se reduce de minutos a segundos y el equipo obtiene visibilidad completa sobre la causa del problema sin revisar registros manualmente.

---

## Estructura del Proyecto

```text
netguard-pro/
├── api/              # Endpoints REST y lógica de autenticación
├── monitor/          # Recolección de métricas (CPU, memoria, disco y red)
├── failover/         # Lógica de detección y conmutación automática
├── firewall/         # Motor de reglas y validación
├── dashboard/        # Frontend del panel (React)
├── docs/             # Documentación técnica
├── tests/            # Pruebas automatizadas
└── docker-compose.yml
```

Cada módulo tiene su propio `README.md` con detalles de implementación. Se recomienda comenzar por `monitor/` y `api/`, ya que son los módulos mejor documentados.

---

## Para Desarrolladores: Integración mediante API

La API REST permite consultar métricas y administrar configuraciones de forma programática.

```bash
curl -X GET "https://api.netguardpro.com/v1/metrics?server=srv-01" \
  -H "Authorization: Bearer SU_TOKEN_AQUI"
```

Respuesta esperada:

```json
{
  "server": "srv-01",
  "cpu_usage": 68.4,
  "latency_ms": 112.3,
  "packet_loss": 0.4
}
```

Documentación completa sobre endpoints, autenticación y límites de solicitudes: [`docs/api.md`](docs/api.md).

---

## Cómo Contribuir

1. **Abra un issue** describiendo el error o la mejora antes de comenzar.
2. **Cree una rama** desde `main`: `feature/nombre-funcionalidad` o `fix/nombre-error`.
3. **Siga los estándares del proyecto:** ESLint para el frontend (`dashboard/`) y PEP 8 para los módulos de Python (`monitor/`, `failover/`).
4. **Escriba pruebas** para cada nueva funcionalidad o corrección (`tests/`).
5. **Abra un Pull Request** incluyendo:
   - Una descripción clara de los cambios realizados y su propósito
   - Referencia al issue relacionado
   - Confirmación de que todas las pruebas fueron aprobadas (`docker compose run tests`)
6. Un mantenedor revisará el PR en un plazo de tres días hábiles.

Guía completa de estilo: [`docs/contributing.md`](docs/contributing.md).

---

## Solución de Problemas

| Problema | Causa probable | Solución |
| --- | --- | --- |
| El panel es lento bajo alta carga | Alto uso de CPU durante análisis avanzados | Reduzca la frecuencia de actualización en `Configuración > Rendimiento` |
| La configuración del firewall es compleja | Curva de aprendizaje de la interfaz | Utilice el asistente guiado en `Firewall > Nuevo Asistente` |
| Demasiadas alertas de seguridad | Se notifican eventos de baja prioridad | Ajuste los niveles de severidad en `Alertas > Prioridades` |
| Transferencias de datos lentas | Congestión del ancho de banda | Active la priorización manual en `Ancho de Banda > Reglas` |

---

## Soporte

- **Documentación completa:** [`docs/`](docs/)
- **Centro de Ayuda:** suporte.netguardpro.com
- **Reportar un error:** Abra un issue en este repositorio
- **Soporte técnico urgente:** suporte@netguardpro.com

---

## Licencia

Este proyecto se distribuye bajo la licencia MIT. Consulte el archivo [`LICENSE`](LICENSE) para más información.
