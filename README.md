#### Project-Prakriti
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
    git clone https://github.com/Kumarharsh1/project-prakriti.git
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
#  Install dependencies
!pip install -U transformers accelerate

#  Authenticate with Hugging Face
from huggingface_hub import login
login(token="your_hf_token_here")  # Replace with your actual token

#  Load IBM's Granite model
from transformers import AutoTokenizer, AutoModelForCausalLM

model_name = "ibm-granite/granite-3b-instruct"  

tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(
    model_name,
    device_map="auto",
    load_in_8bit=True,  # Optional but recommended for memory
    torch_dtype="auto"
)

#  Agent runner function for Granite
def run_agent(agent_role, task_prompt):
    # Format the prompt for the Granite model
    prompt = f"### System: You are an expert {agent_role}.\n\n### User: {task_prompt}\n\n### Assistant:"
    
    inputs = tokenizer.encode(prompt, return_tensors="pt").to(model.device)
    
    outputs = model.generate(
        inputs,
        max_new_tokens=256,
        do_sample=True,
        temperature=0.7,
        top_p=0.9,
        eos_token_id=tokenizer.eos_token_id
    )
    
    response = tokenizer.decode(outputs[0], skip_special_tokens=True)
    # Extract only the assistant's response
    assistant_response = response.split("### Assistant:")[-1].strip()
    
    return assistant_response

#  Define agents and tasks
climate_output = run_agent("Climate Analyst", "Analyze rainfall changes in the Aravalli ecosystem.")
biodiversity_output = run_agent("Biodiversity Strategist", "Identify key endangered species in the Aravallis.")
planner_output = run_agent("Restoration Planner", f"Create a plan using:\nCLIMATE: {climate_output}\nBIO: {biodiversity_output}")

print(" Final Restoration Plan:\n", planner_output)


           #####OR####
### we can use tiiuae/falcon-rw-1b model 

#  Install dependencies
!pip install -U transformers accelerate sentencepiece

#  Import and load an instruction-tuned model
from transformers import AutoTokenizer, AutoModelForCausalLM, pipeline

# Using a small model designed for chatting/instructions
model_name = "TinyLlama/TinyLlama-1.1B-Chat-v1.0"

# Load tokenizer and model
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(
    model_name,
    device_map="auto",  # Automatically uses GPU if available
    load_in_8bit=True,  # Reduces memory usage (may require `bitsandbytes`)
    torch_dtype="auto"   # Automatically handles data type
)

# Create a text generation pipeline
generator = pipeline(
    "text-generation",
    model=model,
    tokenizer=tokenizer,
)

#  Agent runner function using a proper chat template
def run_agent(agent_role, task_prompt):
    # Format the prompt correctly for a chat model
    messages = [
        {"role": "system", "content": f"You are an expert {agent_role}. Provide a concise and helpful answer."},
        {"role": "user", "content": task_prompt}
    ]
    
    # Apply the chat template to format the prompt correctly
    prompt = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
    
    # Generate the response
    outputs = generator(
        prompt,
        max_new_tokens=256,
        do_sample=True,
        temperature=0.7,
        top_k=50,
        top_p=0.95,
        eos_token_id=tokenizer.eos_token_id
    )
    
    # Extract only the assistant's response
    full_response = outputs[0]['generated_text']
    # The response includes the original prompt, so we split it to get only the new part
    assistant_response = full_response.split("assistant\n")[-1].strip()
    
    return assistant_response

#  Agent roles
climate_agent = "Climate Analyst"
biodiversity_agent = "Biodiversity Strategist"
planner_agent = "Restoration Planner"

#  Tasks
climate_task = "Analyze recent rainfall and temperature changes in the dry forest ecosystem of the Aravalli range in India."
biodiversity_task = "Identify key endangered species and biodiversity threats in the dry forests of the Aravalli range."
planner_task = "Propose a detailed restoration plan for the Aravalli forest ecosystem."

#  Run agents
print("Running Climate Agent...")
climate_output = run_agent(climate_agent, climate_task)
print(" Climate Agent:\n", climate_output, "\n" + "="*50 + "\n")

print("Running Biodiversity Agent...")
biodiversity_output = run_agent(biodiversity_agent, biodiversity_task)
print(" Biodiversity Agent:\n", biodiversity_output, "\n" + "="*50 + "\n")

#  Feed outputs into planner
print("Running Restoration Planner...")
planner_task += f"\n\nCLIMATE ANALYSIS: {climate_output}\n\nBIODIVERSITY ASSESSMENT: {biodiversity_output}"
planner_output = run_agent(planner_agent, planner_task)
print(" Restoration Planner:\n", planner_output)





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
