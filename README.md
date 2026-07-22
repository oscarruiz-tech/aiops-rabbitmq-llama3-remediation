## 📐 System Architecture

```text
┌─────────────────────────┐
│  publisher_continuo.py  │  (Infrastructure Telemetry Emitter)
└────────────┬────────────┘
             │ Emits real-time events every 2s via Routing Keys (e.g., europe.database.critical)
             ▼
┌─────────────────────────┐
│   RabbitMQ in Docker    │  (Message Broker w/ Topic Exchange)
└────────────┬────────────┘
             │ Pattern matching & filtering (*.*.critical)
             ▼
┌─────────────────────────┐
│   worker_ai_json.py     │  (Subscriber / AIOps Agent)
└────────────┬────────────┘
             │ Rest API Call on Port 11434 (format="json", temp=0.2)
             ▼
┌─────────────────────────┐
│     Ollama (Llama 3)    │  (Local LLM Inference Engine)
└─────────────────────────┘
```

---

## 🏃‍♂️ Live Demo & Execution

Here is a side-by-side terminal session showing the Telemetry Publisher (right) and the AIOps Worker Agent processing critical events in real-time (left):

<img src="./live_demo.jpg" alt="RabbitMQ and Llama 3 Live Demo" width="100%" />

### 📊 Example Output (Structured JSON Remediation)
