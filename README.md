# Chapter5
This chapter guides you through using memory and callback. Memory and Callbaks are two very important concepts in the agent development

This `README.md` is designed to showcase your architectural mindset. It does explain how to write a LLM agent and run the code; it explains **why** you chose this multi-agent pattern and how the **Google ADK** handles state, reasoning, and tool-use.

---

# 🚗 Friend Trip Agent: root_agent assist a trip planner for friends

An agentic orchestration system built with the **Google Agent Development Kit (ADK)**. This project demonstrates a decoupled, multi-agent architecture designed to help friends to plan a vacation trip.

## 🏗️ Architectural Overview

This project moves away from monolithic prompts by utilizing a **Modular Multi-Agent System**. By separating concerns between specialized agents, we improve reliability, reduce token overhead, and allow for deterministic guardrails.

### The ADK Pipeline
The system utilizes a `LLM-Based Agents` a standalone Intelligent Worker to accomplish a specific task

1.  **Session, State and Memory:** The shared, persistent dictionary (e.g., initial_state) that holds all conversation context, intermediate data, and tool outputs accessible by agents and tools throughout the entire workflow
2.  **before_agent_callback and after_agent_callback:** Custom functions triggered immediately before an orchestrator or specialist agent (like FieldTripLoopAgent) begins its primary execution and after it completes its entire task.
3.  **before_model_callback and after_model_callback:** Functions that intercept and modify the raw instructions or history sent to the generative model and the final output received from the model before the agent uses it.
4.  **before_tool_callback and after_tool_callback:** Specific hooks triggered directly before a tool function (like calculate_cost_tool) is executed to prepare inputs and immediately after it completes to handle the raw outputs.

---

## 🛠️ Technology Stack

* **Framework:** Google Agent Development Kit (ADK) v1.2+
* **Orchestration:** ADK `ParallelAgent` & `InMemoryRunner`
* **Models:** Gemini 2.5 Flash
* **Language:** Python 3.14+
* **Dev Tools:** ADK Web UI (for trace observability)

---

## 📂 Project Structure

```text
Chapter1/
├── agents/
│   ├── __init__.py     # LLM Agent with Search capabilities
│   ├── agent.py        # Logic for EV charging ROI
│   └── .env            # Python-based tools (PSE&G API, Lease Scraper)
├── .adk/               # google ADK tools package
│   
├── .venv/              # libraries and packages
│   
├── .vscode/
│   └── settings.json   # Python manager and package info
└── .env                # GOOGLE_API_KEY and other API keys
```

---

## 🚀 Getting Started

### 1. Prerequisites
Ensure you have a Google AI Studio and python 
```bash
uv init
```

```bash
uv venv
```
```bash
.venv\Scripts\activate.bat	
```

```bash
uv add google-adk 
```

### 2. Running the Agent
You can interact with the concierge via the terminal:
```bash
python agent.py
```

### 3. Visual Debugging (The ADK UI)
To see the "Thought-Action-Observation" loop in real-time, launch the development dashboard:
```bash
adk web
```
*Navigate to `localhost:8080` to view the agentic trace, event logs, and tool execution status.*

---

## 💡 Key Agent Patterns Implemented

### **Tool Decoupling**
Instead of the LLM "hallucinating" trip budget, This tool returns field trip booking confirmation.

### **Stateful Sessions**
Using the `ADK Session` service, the agent remembers user constraints (e.g., "2 friends shows availablity") across multiple turns without needing to re-send the entire chat history in every prompt.


---

## 🛤️ Roadmap
- [ ] **Cloud Deployment:** Migrate from `InMemoryRunner` to `CloudRunner` for deployment on **Vertex AI Agent Engine**.
- [ ] **Multi-Modal Support:** Use Gemini's vision capabilities to analyze places, wether, and other geolocations for vacation trip planner.


---
*Created by Niraj Gupta — Software Architect & AI Enthusiast.*

---

### Why this works for your GitHub:
* **Architectural Language:** Terms like "Decoupled," "Deterministic Guardrails," and "State Management" signal that you are a Software Architect, not just a casual coder.
* **Observability:** Mentioning the `ADK UI` shows you care about debugging and the lifecycle of an application.
* **Extensibility:** The roadmap shows you understand how to scale a local MVP into a production-grade cloud service.
