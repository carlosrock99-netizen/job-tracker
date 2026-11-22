# Job Application Tracker

Extensão de navegador (**Manifest V3**) integrada a uma API local em **Python (FastAPI + SQLite)** para capturar, centralizar e gerenciar candidaturas de emprego automaticamente no **LinkedIn**, **Gupy**, **Indeed** e portais externos.

## Funcionalidades

- **Captura Automática via DOM:** Detecta cliques nos botões de envio de candidatura e extrai cargo, empresa, localização, modelo de trabalho (`Remoto`, `Híbrido`, `Presencial`), regime (`CLT`, `PJ`, `Estágio`) e faixa salarial.
- **Resiliência Offline (Offline-First):** Caso o backend esteja desligado, as candidaturas são armazenadas na fila local (`chrome.storage.local`) com badge contador no ícone e sincronizadas automaticamente via `chrome.alarms`.
- **Atalho Universal (`Alt + S`):** Captura vagas em qualquer site externo (Greenhouse, Lever, Workday, etc.).
- **Dashboard Web + Exportação CSV:** Painel interativo em `http://localhost:8000` com indicadores de conversão, filtros combinados, edição inline de status/notas e exportação para planilha.

## Como Executar

### 1. Backend (Windows — 1 Clique)
1. Extraia o arquivo ZIP.
2. Dê um duplo clique em **`iniciar.bat`**. Caso você não tenha o Python instalado, o script informa exatamente o que será instalado (Python 3.12, ambiente virtual `venv` e bibliotecas FastAPI/Uvicorn/Pydantic), solicita sua confirmação (`S/N`), realiza a instalação automaticamente e abre o painel no navegador.
*(Opcional: execute `python backend/seed.py` para popular o banco com vagas de demonstração).*

### 2. Extensão (Chrome / Opera / Edge / Brave)
1. Abra `chrome://extensions` (ou `opera://extensions`).
2. Ative o **Modo do desenvolvedor**.
3. Clique em **Carregar sem compactação** e selecione a pasta **`extension/`**.

## Arquitetura

```text
job-tracker-automation/
├── extension/
│   ├── manifest.json     # Manifest V3 + permissões
│   ├── content.js        # Extratores por plataforma + cache SPA + toast visual
│   ├── background.js     # Service Worker + fila offline + sync periódico
│   ├── popup.html / .js  # Mini-painel rápido no ícone da extensão
│   └── welcome.html/.js  # Onboarding e teste de conexão
├── backend/
│   ├── main.py           # FastAPI + SQLite + Dashboard HTML + Export CSV
│   ├── seed.py           # Popula dados de exemplo
│   └── requirements.txt
├── iniciar.bat           # Launcher automático para Windows
└── iniciar.sh            # Launcher para Linux/macOS
```
