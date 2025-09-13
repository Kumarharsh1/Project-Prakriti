![Project Prakriti](https://img.shields.io/badge/Project-Prakriti-green)
![AI Agents](https://img.shields.io/badge/Multi--Agent-System-blue)
![Climate Analysis](https://img.shields.io/badge/Climate-Analysis-orange)
![Biodiversity](https://img.shields.io/badge/Biodiversity-Assessment-brightgreen)

**Project Prakriti** is an advanced multi-agent AI system designed for comprehensive climate analysis, biodiversity assessment, and ecological restoration planning. By integrating **Groq API** and **IBM WatsonX API**, it generates expert insights and provides rich visualizations to track ecological restoration impacts.

## 🌟 Key Features

- **Multi-Agent Workflow**
  - **Climate Analyst Agent** → Analyzes rainfall patterns, temperature trends, and climate risks
  - **Biodiversity Strategist Agent** → Evaluates species status, threats, and conservation opportunities
  - **Restoration Planner Agent** → Generates detailed restoration plans with native species recommendations and monitoring schedules

- **Comprehensive Visualizations**
  - Biodiversity improvement bar charts
  - Rainfall trend comparison line charts
  - Native species distribution pie charts
  - Forest cover before/after restoration scatter plots
  - Regional forest cover change heatmaps

- **Resilient API Architecture**
  - Primary: **Groq API** for high-performance inference
  - Fallback: **IBM WatsonX API** for reliable backup processing

## 🏗️ System Architecture

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



## 🛠️ Tech Stack

- **Language:** Python 3.11+
- **APIs:** Groq, IBM WatsonX
- **Libraries:**
  - `requests` → API calls
  - `pandas`, `numpy` → data handling
  - `matplotlib`, `seaborn` → data visualization
  - `json`, `csv` → data processing

## 📦 Installation

```bash
# Clone the repository
git clone https://github.com/your-username/project-prakriti.git
cd project-prakriti

# Install dependencies
pip install -r requirements.txt

▶️ Run the Project
python prakriti.py

🔮 Future Enhancements
Integrate NASA MODIS NDVI dataset for real vegetation greenness
Use live climate APIs instead of static inputs
Add GIS-based maps for restoration zones
Build a community portal for citizen participation

👨‍💻 Contributors
Kumar Harsh → Lead Developer & Researcher








