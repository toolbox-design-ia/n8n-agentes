# Automatización agéntica con n8n — Material del libro

Repositorio companion del libro **«Automatización agéntica con n8n»**
(Henry Ramírez Reyes, serie INTELIGENCIA ARTIFICIAL, Toolbox Design).

Aquí viven los workflows del libro, exportados en JSON y listos para
importar en n8n. El Anexo A del libro explica, paso a paso y sin
experiencia previa, cómo descargar este repositorio y cómo importar un
workflow.

## Cómo usar este repositorio

1. Descarga el repositorio: botón verde **Code → Download ZIP** (no hace
   falta cuenta de GitHub) y descomprime el archivo.
2. En n8n: **Workflows → Import from File** y elige el `.json` del
   capítulo que estés leyendo.
3. Revisa las credenciales que el workflow necesita (cada carpeta lo
   indica en su README).

## Instalación de n8n (`infra/`)

La carpeta `infra/` trae la instalación que el libro describe, lista para usar:

| Archivo | Para qué sirve |
| --- | --- |
| `infra/docker-compose.yml` | n8n + PostgreSQL, la instalación mínima del capítulo 2 |
| `infra/docker-compose.queue.yml` | Añade Redis y un worker: el modo queue del capítulo 16 |
| `infra/.env.example` | Plantilla de variables; cópiala a `infra/.env` y rellénala |

```bash
cd infra
cp .env.example .env      # y edita los valores
docker compose up -d
# modo queue (cap. 16):
# docker compose -f docker-compose.yml -f docker-compose.queue.yml up -d
```

Después, n8n queda en `http://localhost:5678`. Si la interfaz carga pero no
deja iniciar sesión, o el disparador programado se ejecuta a otra hora, mira
[`docs/troubleshooting.md`](docs/troubleshooting.md).

## Correspondencia capítulo → workflow

Cada capítulo del libro se cierra con una caja **«En el repositorio»** que
nombra sus archivos y dice qué hay en cada uno. Esta tabla es el índice de
todas ellas. Los capítulos que no aparecen aquí (1, 2, 14, 16, 17, 18 y los
anexos) no traen workflow propio: tratan instalación, criterio de negocio o
disciplina de operación, no un flujo que importar.

| Capítulo | Carpeta | Archivos |
| --- | --- | --- |
| 3. El lenguaje de los flujos | `workflows/03_lenguaje/` | `03_flujo_basico.json`, `03_error_workflow.json` |
| 4. Conectar el mundo | `workflows/04_conectar/` | `04_api_sin_credenciales.json` |
| 5. El nodo de agente por dentro | `workflows/05_agente/` | `05_agente_basico.json` |
| 6. Herramientas para el agente | `workflows/06_herramientas/` | `06_herramienta_inventario.json`, `06_agente_con_herramienta.json` |
| 7. Memoria y contexto | `workflows/07_memoria/` | `07_memoria_postgres.json`, `07_esquema.sql` |
| 8. RAG en n8n | `workflows/08_rag/` | `08_ingesta.json`, `08_consulta.json` |
| 9. MCP y el ecosistema | `workflows/09_mcp/` | `09_logica_cotizacion.json`, `09_servidor_mcp.json`, `09_cliente_mcp.json` |
| 10. Proyecto: el asistente interno | `workflows/10_asistente/` | `10_asistente_interno.json`, `10_esquema.sql` |
| 11. Patrones de producción | `workflows/11_patrones/` | `11_idempotencia_reintentos.json`, `11_esquema.sql` |
| 12. Multi-agente en n8n | `workflows/12_multiagente/` | `12_orquestador.json` |
| 13. Canales | `workflows/13_canales/` | `13_multicanal.json` |
| 15. Proyecto: atención a clientes multicanal | `workflows/15_atencion/` | `15_atencion_clientes.json`, `15_esquema.sql` |
| 19. Proyecto: el proceso completo | `workflows/19_proceso/` | `19_proceso_completo.json`, `19_informe_semanal.json`, `19_esquema.sql` |

**Estado de pruebas.** Los 19 workflows se importaron en una instancia real de n8n 2.19.5 (19/19 importados sin errores, todos los tipos de nodo verificados contra la instalación) y el flujo del capítulo 4 se ejecutó de principio a fin contra la API real. Los que usan credenciales (Ollama, PostgreSQL, Qdrant, IMAP...) requieren configurarlas tras importar: cada carpeta indica cuáles.

## Licencia

MIT para los workflows y el código. El texto del libro tiene todos los
derechos reservados.
