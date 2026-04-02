# Crumble: Stateful AI Ordering Agent 🍪

A headless, full-stack AI chatbot designed for Crumble. This project demonstrates advanced LLM orchestration, separating frontend UI from a deterministic, asynchronous AI backend.
<img width="495" height="704" alt="ss1" src="https://github.com/user-attachments/assets/bd464e00-ace6-46fe-ae14-ff60f4eea798" />

---

## 🧠 Architecture Overview

This project uses a **Headless AI Architecture**:
* **Frontend:** Vanilla JavaScript/HTML chat widget implementing local session management and asynchronous typing UI states.
* **Backend:** [n8n](https://n8n.io/) (Node-based Automation) acting as the orchestration layer.
* **Database:** Google Sheets for persistent session memory.
* **LLM Engine:** Google Gemini 2.5 for entity extraction and persona generation.

---

## ⚡ Key Engineering Features

1. **State Management & Memory:** Bypasses standard LLM "goldfish memory" by generating unique `sessionIds` in the browser, routing them through Webhooks, and appending/retrieving conversation history from an external database in real-time.
2. **Hybrid Logic Pipeline:** Separates probabilistic logic (the LLM extracting order items) from deterministic logic (native JS calculating the exact bill total) to strictly prevent AI math hallucinations.
3. **Race Condition Mitigation:** Architected a sequential data pipeline (`Listen` ➔ `Extract` ➔ `Calculate` ➔ `Fetch Memory` ➔ `Respond`) to ensure background database writes do not block the UI response.
4. **Graceful Fallbacks:** Custom `Memory Engine` script handles empty database states (brand new users) without crashing the pipeline or sending empty objects to the visual nodes.

---

## 🛠️ How to Run Locally

### 1. Frontend
* Open `frontend/index.html` in any modern web browser or run via a local server (e.g., VS Code Live Server).

### 2. Backend<img width="1920" height="934" alt="Screenshot (68)" src="https://github.com/user-attachments/assets/da13fb35-8943-4db6-b965-21c61bb05393" />

* Install [n8n](https://n8n.io/).
* Open n8n, create a new workflow, and click **"Import from File"**.
* Select the `backend/crumble-agent-workflow.json` file.
* Update the Google Sheets nodes with your own credentials and sheet ID.
* Change the Webhook node to use a **"Production URL"** and activate the workflow.

---

<p align="center">
  <i>Built with ❤️ for Crumble</i>
</p>
