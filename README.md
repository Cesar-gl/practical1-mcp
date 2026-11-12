# Práctica 1 - Model Context Protocol (MCP)

## 1. Descripción
Esta práctica consistió en configurar y utilizar servidores MCP (Model Context Protocol) en el agente de programación Google Antigravity (IDE). Se exploraron las capacidades de los servidores `filesystem` y `playwright`, y se añadió un tercer servidor (`memory`) para resolver tareas específicas.

## 2. Requisitos y reproducción
Para reproducir esta práctica necesitas:
- Node.js v18 o superior.
- Git.
- Google Chrome.
- Google Antigravity (IDE).
- Una cuenta de GitHub.

**Pasos para reproducir:**
1. Clona este repositorio.
2. Abre la carpeta en Antigravity.
3. Modifica el archivo `.agents/mcp_config.json` y cambia la ruta en el servidor `filesystem` por la ruta absoluta de tu carpeta local.
4. Reinicia Antigravity para que detecte los servidores.

## 3. Servidores MCP
Se configuraron 3 servidores en `.agents/mcp_config.json`:
- **filesystem:** Permite leer, escribir y listar archivos dentro de la carpeta de la práctica.
- **playwright:** Permite controlar un navegador Chrome (navegar, hacer clic, capturas).
- **memory:** (Actividad D) Permite guardar y consultar información en un grafo de conocimiento.

## 4. Actividades

### Actividad A (filesystem)
- **Instrucción:** Listar datos, leer el CSV, calcular promedios y generar `salida/reporte.md`.
- **Herramientas usadas:** `filesystem/list_directory`, `filesystem/read_text_file`, `filesystem/write_file`.
- **Resultado:** Se creó el reporte con 8 alumnos, 6 aprobados, 2 reprobados y un promedio general de 7.50.
- **Evidencia:** ![Actividad A](evidencias/02_actividad_a.png)

### Actividad B (playwright + filesystem)
- **Instrucción:** Abrir la página de Wikipedia, extraer la tabla de entidades, guardar el CSV y tomar captura.
- **Herramientas usadas:** `playwright/browser_navigate`, `playwright/browser_evaluate`, `filesystem/write_file`, `playwright/browser_take_screenshot`, `playwright/browser_close`.
- **Resultado:** Se generó `salida/entidades.csv` con 32 filas. La primera entidad es Chihuahua con 247455 km². El agente indicó que la población es de 2020.
- **Verificación manual:** Se compararon 3 filas al azar con la página web original, confirmando que los datos coinciden.
- **Evidencias:** ![Navegador](evidencias/03_actividad_b_navegador.png) y ![Verificación](evidencias/04_actividad_b_verificacion.png)

### Actividad C (límites del servidor)
- **Instrucción:** Probar los límites del servidor intentando leer archivos fuera de la carpeta y listar el directorio padre.
- **Herramientas usadas:** `filesystem/list_allowed_directories`, `filesystem/read_text_file`, `filesystem/list_directory`.
- **Resultado:** El servidor bloqueó los intentos con el siguiente mensaje exacto:
> `Encountered error in tool execution: Access denied - path outside allowed directories: C:\Users\Daniel A. Sanchez S\Desktop not in C:\Users\Daniel A. Sanchez S\Desktop\practical-mcp`
- **Conclusión:** El límite lo impone **el servidor MCP**, no el modelo, lo cual es fundamental para la seguridad.
- **Evidencia:** ![Actividad C](evidencias/05_actividad_c.png)

### Actividad D (Tercer servidor: memory)
- **Servidor elegido:** `@modelcontextprotocol/server-memory` (publicado por Anthropic y los mantenedores del protocolo MCP).
- **Tarea:** Crear una entidad llamada "Practica MCP" con una observación y luego buscarla.
- **Herramientas usadas:** `memory/create_entities`, `memory/open_nodes`.
- **Por qué es confiable:** Es un servidor oficial mantenido en el repositorio oficial de Model Context Protocol, lo que garantiza su autenticidad y seguridad.
- **Evidencia:** ![Actividad D](evidencias/06_actividad_d.png)

## 5. Problemas encontrados
Durante la configuración inicial, el agente borró accidentalmente el servidor `filesystem` del archivo `mcp_config.json`. Se solucionó volviendo a pegar la configuración correcta y verificando que no hubiera errores de sintaxis en el JSON.

## 6. Fuentes
- Documentación del protocolo: https://modelcontextprotocol.io
- Servidor filesystem: https://github.com/modelcontextprotocol/servers
- Servidor playwright: https://github.com/microsoft/playwright-mcp
- Wikipedia (Actividad B): https://es.wikipedia.org/?curid=5897912