+-------------------+     +-----------------------------+
|                   |     | KNOWLEDGE BASE              |
|  CLIMATE API      |     | (Vector DB with             |
| (e.g., IMD, NASA) +-----> ISFR Reports, Species Data) |
|                   |     |                             |
+-------------------+     +-------------+---------------+
          ^                             ^
          |                             |
+---------+---------+       +-----------+-----------+
| Climate Analyst   |       | Biodiversity Strategist|
| Agent             |       | Agent                 |
| (IBM Granite-7B + ADK)    | (IBM Granite-7B + ADK) |
+---------+---------+       +-----------+-----------+
          ^                             ^
          |                             |
          +--------------+--------------+
                         |
                         v
               +---------+---------+
               | Restoration Planner|
               | Agent             |
               | (IBM Granite-7B + ADK) |
               +---------+---------+
                         |
                         v
               +---------+---------+
               | STRUCTURED PLAN   |
               | (JSON / PDF)      |
               +-------------------+




# Project-Prakriti
# Project Prakriti: An Agentic AI Framework for Precision Ecological Restoration

[![Built with IBM ADK](https://img.shields.io/badge/Built%20with-IBM%20ADK-blue.svg)](https://github.com/IBM/agent-development-kit)
[![Hackathon](https://img.shields.io/badge/India-AI%20Impact%20Hackathon-orange.svg)](https://iisc-ibm-india-ai-impact.devpost.com/)

##  Overview

Project Prakriti is a proof-of-concept for a multi-agent AI system designed to automate the creation of data-driven ecological restoration plans tailored for India's unique ecosystems. It leverages the power of Agentic AI, where specialized models collaborate like a team of experts to tackle the complex problem of land degradation and biodiversity loss.

This project was developed as a proposal for the **India AI Impact Generative AI Hackathon** (Track 3: Agentic AI).

##  Architecture

Project Prakriti is built on a foundation of IBM's open-source technologies and follows a multi-agent workflow:

1.  **Climate Analyst Agent**: Analyzes historical climate data for a target region.
2.  **Biodiversity Strategist Agent**: Identifies key native and endangered species by querying a knowledge base.
3.  **Restoration Planner Agent**: Synthesizes all inputs to generate a comprehensive, actionable restoration plan.

**High-Level Architecture:**
*(You can place the architecture diagram you create here)*
![Project Prakriti Architecture](./assets/architecture-diagram.png) <!-- Link to your image -->

##  Built With

*   **Programming Language:** Python
*   **Framework & Orchestration:** IBM Agent Development Kit (ADK)
*   **Foundation Models:** IBM Granite-7B-Instruct
*   **Libraries:** Hugging Face Transformers, LangChain
*   **Knowledge Management:** ChromaDB (Vector Database)
*   **Data Sources:** Indian Meteorological Department (IMD), Indian State of Forest Report (ISFR)

##  Getting Started (Proof of Concept)

This repository contains an initial proof-of-concept (PoC) built with a non-IBM model to demonstrate the core multi-agent concept. The final implementation will migrate to the full IBM tech stack on Kaggle.

### Prerequisites

*   Python 3.8+
*   A Hugging Face account and access token (for model access)
*   `pip`

### Installation & Run

1.  **Clone the repo**
    ```bash
    git clone https://github.com/YOUR_USERNAME/project-prakriti.git
    cd project-prakriti
    ```

2.  **Install dependencies**
    ```bash
    pip install -U transformers accelerate sentencepiece huggingface_hub
    ```

3.  **Run the PoC script**
    ```bash
    python poc_agentic_workflow.py
    ```

### Proof of Concept Code

The core logic of the multi-agent workflow is demonstrated in the PoC script:

```python
# Install dependencies
# !pip install -U transformers accelerate sentencepiece huggingface_hub

# Authenticate
from huggingface_hub import login
login(token="your_hf_token_here")

#  Load model and tokenizer
from transformers import AutoTokenizer, AutoModelForCausalLM

model_name = "meta-llama/Llama-2-7b-chat-hf"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name, device_map="auto")

#  Agent runner function
def run_agent(agent_role, task_prompt):
    messages = [
        {"role": "system", "content": f"You are a helpful assistant acting as a {agent_role}."},
        {"role": "user", "content": task_prompt}
    ]
    inputs = tokenizer.apply_chat_template(
        messages,
        add_generation_prompt=True,
        return_tensors="pt"
    ).to(model.device)
    outputs = model.generate(**inputs, max_new_tokens=300)
    response = tokenizer.decode(outputs[0][inputs["input_ids"].shape[-1]:], skip_special_tokens=True)
    return response

# Define agents and tasks
climate_output = run_agent("Climate Analyst", "Analyze rainfall changes in the Aravalli ecosystem.")
biodiversity_output = run_agent("Biodiversity Strategist", "Identify key endangered species in the Aravallis.")
planner_output = run_agent("Restoration Planner", f"Create a plan using:\nCLIMATE: {climate_output}\nBIO: {biodiversity_output}")

print("📋 Final Restoration Plan:\n", planner_output)
