# Claude Quickstarts

## Qué es
Colección de proyectos de referencia para que developers arranquen rápido con la Claude API. Cada quickstart es una base lista para customizar: computer-use, browser-use, customer support, financial analyst, autonomous coding, Managed Agents.

## Cómo se levanta

```bash
# Computer-Use Demo (Docker)
cd computer-use-demo
./setup.sh
docker build . -t computer-use-demo:local
docker run -e ANTHROPIC_API_KEY=$ANTHROPIC_API_KEY \
  -v $(pwd)/computer_use_demo:/home/computeruse/computer_use_demo/ \
  -p 5900:5900 -p 8501:8501 -p 6080:6080 -p 8080:8080 \
  -it computer-use-demo:local

# Customer Support Agent / Financial Data Analyst (Node)
cd <quickstart-dir>
npm install && npm run dev

# Autonomous Coding / Managed Agents (Python)
cd <quickstart-dir>
uv sync && uv run python main.py
```

## Stack
- Python 3 + uv (computer-use, autonomous-coding, managed-agents)
- TypeScript / Next.js (customer-support-agent, financial-data-analyst, browser-use-demo)
- Docker (computer-use-demo)
- Ruff + pyright (Python linting/typecheck)
- ESLint + shadcn/ui (TS quickstarts)

## Estructura
```
computer-use-demo/          — control de desktop vía Docker + VNC
computer-use-best-practices/ — implementación nativa macOS (correr en VM)
browser-use-demo/           — automatización web con Playwright
customer-support-agent/     — agente de soporte con knowledge base (Next.js)
financial-data-analyst/     — análisis financiero con visualización (Next.js + Recharts)
autonomous-coding/          — agente de coding autónomo (Claude Agent SDK)
managed-agents/             — quickstarts de Managed Agents (chat-sdk, copilot-kit, knowledge-wiki)
agents/                     — definiciones de agentes compartidas
```

## Reglas de este proyecto
- Instancias del SDK de Anthropic siempre se llaman `client` — `const client = new Anthropic()` / `client = Anthropic()`. En código Y en READMEs.
- Nunca usar el acrónimo "CMA". Escribir "Managed Agents" o "Claude Managed Agents" en prose, comentarios e identificadores.
- Cambios en archivos con copyright notice: agregar entrada en el `CHANGELOG.md` del subdirectorio.
- Python: snake_case para funciones/variables, PascalCase para clases. Type annotations en todos los parámetros y returns.
- TypeScript: strict mode. Function components con React hooks. shadcn/ui para UI components.
- Correr lint/format antes de commitear:
  - Python: `ruff check . && ruff format . && pyright`
  - Node: `npm run lint && npm run build`

## Cosas que ya intentamos y no funcionaron
- Usar "CMA" como abreviatura — prohibido en el repo. Siempre expandir.
- Omitir type annotations en Python — pyright las requiere.
