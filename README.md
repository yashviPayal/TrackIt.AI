#  TrackIt.AI: Autonomous Habit Tracker

**Status:** Prototype / Demonstration
**Core Concepts:** LLM-Powered Agent, Custom Tools, Sessions & State Management

---

## Overview: Solving the Habit Friction Gap

**The Problem:** Habit tracking often fails due to the **Friction Gap**—the small, critical effort required to manually log data is too high when motivation is low. Users quit because the app feels like homework.

**The Solution:** We built an intelligent **LLM-Powered Agent** that eliminates this friction. It transforms ambiguous natural language ("I only did 5 minutes of reading") into a reliable, state-altering command. This shifts the application's utility from passive data recording to **active, adaptive coaching**, maximizing user motivation and ensuring sustainable behavioral change.

---

##  Architecture: The LLM-Tool-State Loop

The Agent operates on a fixed, sequential loop, leveraging the power of Groq's high-speed inference for real-time interaction.
![Banner](./assets/architecture.jpg)

### 1. Why Agents?

A standard LLM is a brilliant *brain*, but it can't securely update a database. The Agent acts as the **orchestrator**, using the LLM for reasoning and delegating transactional updates to **Custom Tools**. This structure ensures the system is **stateful, secure, and integrated**.

### 2. Workflow Diagram

**[Insert Architecture Diagram URL Here (e.g., Static or Animated Image)]**

| Step | Component & Concept | Description |
| :--- | :--- | :--- |
| **1. Classification** | **LLM Classifier (Groq)** | Parses messy input into a structured JSON command (Intent, Habit, Value). Uses a low temperature ($T=0.0$) for reliability. |
| **2. Tool Execution** | **Custom Tools (Python Functions)** | Calls secure functions (`update_streak_and_history`) based on the intent. This is where business logic (like streak checks) executes. |
| **3. State Management** | **Session State (`HABIT_STORE`)** | The Custom Tool writes the new data (e.g., streak = 4) to this persistent in-memory dictionary. |
| **4. NLG Response** | **LLM & Context** | The agent injects the updated state and adaptive context (e.g., the 2-Minute Rule) back into the LLM to generate a personalized, motivating response ($T=0.7$). |

---

## Technology Stack

| Component | Technology Used | Role in the Agent Architecture |
| :--- | :--- | :--- |
| **LLM-Powered Agent** | **Groq API** (`llama-3.1-8b-instant`) | **Low-latency inference** engine for real-time decision-making. |
| **Core Logic/Orchestration** | **Python** (Custom Classes and Functions) | Manages the **sequential agent loop** and flow control. |
| **Custom Tools** | **Python Functions** | Encapsulate **secure business logic** and state interaction. |
| **Session State Management** | **Python Dictionary** (`HABIT_STORE`) | Stores the persistent user data (streaks, history) during the session. |
| **User Interface (UI)** | **Gradio** | Provides the interactive chat and dashboard visualization. |

---

## Future Works and Roadmap

1.  **Passive Data Integration (Smartwatch APIs):** Integrate a **Custom Tool** to pull passive data (steps, sleep) from external APIs, moving the agent from reactive to **proactive**.
2.  **Voice Input with Custom Wake Word:** Implement **ASR** and **VAD** for truly **zero-friction, ambient interaction**.
3.  **Agent Observability and Evaluation:** Implement comprehensive logging to track **Agent Latency** and **Classification Accuracy** for data-driven tuning.
4.  **Long-Term Memory:** Implement **Context Compaction** to allow the agent to recall deep history for more empathetic coaching.

---

## Setup and Installation Instructions

### Prerequisites

1.  **Python 3.8+**
2.  **Groq API Key:** Required for LLM communication.

### 1. Installation

```bash
# Clone the repository
git clone [YOUR_REPO_URL]
cd trackit-ai

# Install required libraries
pip install groq gradio pandas
```
### 3. Run the Agent

```bash
python ui.py
```

The Gradio UI will open automatically.

---

## Try These Examples

| Input | Expected Behavior |
|-------|-------------------|
| `I completed walking 700 steps today.` | Updates walking streak |
| `I did 12 minutes of meditation.` | Updates meditation streak |
| `I'm feeling lazy about reading.` | Trigger 2-Minute Rule coaching |
| `Show my habits` | Returns current dashboard |

---
## Made With Help Of
Youtube Tutorials, Gen-AI and similar resources provided under competition.

---
## ❤️ Credits

Built for productive but lazy people everywhere —  
because **doing the habit should matter more than logging it.**
