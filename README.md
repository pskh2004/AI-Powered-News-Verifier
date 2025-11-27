
# AI-Powered News Verifier

A Jupyter-friendly, multi-agent fake news detection system built using the **AI Development Kit (ADK)**. 

Inspired by the Google x Kaggle AI Intensive course, this project demonstrates how to assemble conversational agents, real-time tool integrations, and shared memory into a coherent fact-checking pipeline.

## 📖 Overview

The goal of this system is to automate the verification of news claims. When provided with a headline or statement, it employs a team of AI agents to investigate real-time Google Search results, compare sources, reason about consistency, and deliver a final verdict on the claim's legitimacy.

This implementation is optimized for **Jupyter Notebooks**, addressing common asynchronous execution issues (event loop conflicts) while utilizing ADK sessions to maintain context like a dedicated investigator.

## ✨ Key Features

### 🤖 Multi-Agent Architecture
The logic is divided among three specialized agents:
*   **Search Agent:** Utilizes the `google_search` tool to fetch multiple independent, real-world sources.
*   **Analysis Agent:** parsing the collected search results to extract factual signals and context.
*   **Verdict Agent:** Synthesizes the analysis to classify the news as **Likely Real**, **Suspected Misinformation**, or **Inconclusive**.

### 🧠 Shared Session Memory
Using ADK Sessions, the system maintains a "journal" of the investigation, tracking:
*   The initial user claim.
*   Raw search results.
*   Inter-agent communication.
*   The final reasoning chain.

### ⚡ Notebook-Friendly Async
Designed to avoid `RuntimeError: This event loop is already running` issues common in interactive environments. The system allows you to simply run:
```python
await fact_check_claim("your claim here")
```

### 🔍 Explainable AI
The system doesn't just give a Yes/No answer. It provides:
*   A summary of findings.
*   Step-by-step reasoning.
*   Confidence levels.
*   Links to the sources used.

## 🛠️ Installation

1.  **Install the required dependencies:**

```bash
pip install google-generativeai kaggle-adk nest_asyncio
```

2.  **API Configuration:**
    You must have a valid Google GenAI API key. Set this up in your environment variables or securely within your notebook secrets.

## 🚀 Usage

Here is how to run the verifier inside a Jupyter Notebook:

```python
import nest_asyncio
from kaggle_adk import ADK, Session

# Apply the patch to allow nested event loops in notebooks
nest_asyncio.apply()

# Define your API Key (Example using Kaggle Secrets)
# from kaggle_secrets import UserSecretsClient
# user_secrets = UserSecretsClient() 
# GOOGLE_API_KEY = user_secrets.get_secret("GOOGLE_API_KEY")

# Run the verifier
claim = "NASA discovered a second moon orbiting Earth last week."
result = await fact_check_claim(claim)

print(result)
```

## ⚙️ How It Works

1.  **Input:** The user feeds a specific claim to the system.
2.  **Investigation:** The **Search Agent** queries the web for recent, authoritative data.
3.  **Extraction:** The **Analysis Agent** filters noise and identifies corroborating or conflicting evidence.
4.  **Decision:** The **Verdict Agent** reviews the evidence and creates a final report.
5.  **Output:** The user receives a comprehensive verification report.

## 📂 Project Structure

```text
├── notebook.ipynb              # Main entry point for running the system
├── news_verification_agents.py # Modular agent logic and definitions
├── thumbnail.png               # Project visualization
└── README.md                   # Project documentation
```

## 🤝 Contributing

Feel free to fork this repository and submit pull requests. Suggestions for adding new tools (e.g., image verification or specific fact-checking API integrations) are welcome.

## 📄 License

[MIT License](LICENSE)
