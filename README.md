# **Project Prakriti: An Agentic AI Framework for Precision Ecological Restoration**

[![Built with IBM ADK](https://img.shields.io/badge/Built%20with-IBM%20ADK-blue.svg)](https://github.com/IBM/agent-development-kit)  
[![Hackathon](https://img.shields.io/badge/India-AI%20Impact%20Hackathon-orange.svg)](https://iisc-ibm-india-ai-impact.devpost.com/)

##  Overview

**Project Prakriti** is a proof-of-concept for a multi-agent AI system designed to automate the creation of data-driven ecological restoration plans tailored for India's unique ecosystems. It leverages the power of Agentic AI, where specialized models collaborate like a team of experts to tackle the complex problem of land degradation and biodiversity loss.

This project was developed as a proposal for the **India AI Impact Generative AI Hackathon** (Track 3: Agentic AI).

##  Architecture

Project Prakriti is built on a foundation of IBM's open-source technologies and follows a multi-agent workflow:

1. **Climate Analyst Agent**: Analyzes historical climate data for a target region.  
2. **Biodiversity Strategist Agent**: Identifies key native and endangered species by querying a knowledge base.  
3. **Restoration Planner Agent**: Synthesizes all inputs to generate a comprehensive, actionable restoration plan.

### High-Level Architecture

'''
          
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
               | (IBM Granite-7B + ADK)|
               +---------+---------+
                         |
                         v
               +---------+---------+
               | STRUCTURED PLAN   |
               | (JSON / PDF)      |
               +-------------------+

                                       '''


##  Tech Stack

- **Language:** Python 3.11+
- **APIs:** Groq, IBM WatsonX
- **Libraries:**
  - `requests` → API calls
  - `pandas`, `numpy` → data handling
  - `matplotlib`, `seaborn` → data visualization
  - `json`, `csv` → data processing

##  Installation & Setup

#### Clone the repository
git clone https://github.com/your-username/project-prakriti.git
cd project-prakriti

#### Create virtual environment
python -m venv prakriti-env
source prakriti-env/bin/activate  # On Windows: prakriti-env\Scripts\activate

#### Install dependencies
pip install -r requirements.txt

#### Set up environment variables
cp .env.example .env

#### Add your API keys to the .env file

## Key Features*

* **Multi-Agent Workflow**
* **Climate Analyst Agent** → Analyzes rainfall patterns, temperature trends, and climate risks
* **Biodiversity Strategist Agent** → Evaluates species status, threats, and conservation opportunities
* **Restoration Planner Agent** → Generates detailed restoration plans with native species recommendations and monitoring schedules

- **Comprehensive Visualizations**
  * Biodiversity improvement bar charts
  * Rainfall trend comparison line charts
  *  Native species distribution pie charts
  * Forest cover before/after restoration scatter plots
  * Regional forest cover change heatmaps

- **Resilient API Architecture**
  * Primary: **Groq API** for high-performance inference
  * Fallback: **IBM WatsonX API** for reliable backup processing

## Run the main application
python prakriti.py

## Or run with specific region
python prakriti.py --region "Madhya Pradesh"

## Generate report only
python prakriti.py --report-only

## Select a region (e.g., Madhya Pradesh, Maharashtra, Karnataka)

* Climate Agent generates insights on rainfall, temperature, and climate risks

* Biodiversity Agent uses climate analysis to assess species status and threats

* Restoration Agent combines insights to propose a comprehensive restoration plan

* Visualizations display before/after comparisons of biodiversity and forest coverUsage

## Output

### Climate Analysis Complete:
* Average Rainfall: 1200 mm/year
* Temperature Range: 18°C - 35°C
* Identified Risks: Soil erosion, water scarcity

### Biodiversity Assessment:
* Native Species: 45 identified
* Endangered Species: 12 need protection
* Conservation Opportunities: 8 zones identified

 ### Restoration Plan Generated:
* Recommended Species: 15 native varieties
* Planting Schedule: Monsoon season optimal
* Monitoring Protocol: Quarterly assessments


## Future Enhancements
  
* Integrate NASA MODIS NDVI dataset for real vegetation greenness
* Use live climate APIs instead of static inputs
* Add GIS-based maps for restoration zones
* Build a community portal for citizen participation
* Implement blockchain for transparent fund allocation
* Add drone imagery analysis for progress monitoring

### Contributors
Kumar Harsh → Lead Developer & Researcher

## Together, let's build a greener future! 🌱

