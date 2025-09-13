#  Project Prakriti  

**Project Prakriti** is a multi-agent AI system for **climate analysis, biodiversity assessment, and ecological restoration planning**.  
It integrates **Groq API** and **IBM WatsonX API** to generate expert insights, and provides rich **visualizations** to track ecological restoration impacts.  

---

##  Features  

-  **Multi-Agent Workflow**  
  - **Climate Agent** → Analyzes rainfall, temperature, and risks.  
  - **Biodiversity Agent** → Evaluates species status, threats, and opportunities.  
  - **Restoration Agent** → Generates restoration plans (native species, planting schedule, monitoring).  

-  **Visualizations**  
  - Bar chart → Biodiversity improvement  
  - Line chart → Rainfall trend comparison  
  - Pie chart → Native species distribution  
  - Scatter plot → Forest cover before vs after restoration  
  - Heatmap → Forest cover change across regions  

-  **Resilient API Calls**  
  - Primary: **Groq API**  
  - Fallback: **IBM WatsonX API**  

---

##  Tech Stack  

- **Language:** Python 3.11+  
- **APIs:** Groq, IBM WatsonX  
- **Libraries:**  
  - `requests` → API calls  
  - `pandas`, `numpy` → data handling  
  - `matplotlib`, `seaborn` → data visualization  

---

##  How It Works  

1. **Select a region** (e.g., Madhya Pradesh, Maharashtra, Karnataka).  
2. **Climate Agent** generates insights on rainfall, temperature, risks.  
3. **Biodiversity Agent** uses climate analysis to assess species and threats.  
4. **Restoration Agent** combines both to propose a restoration plan.  
5. **Visualizations** show before/after comparisons of biodiversity and forest cover.  

---

##  Sample Visualizations  

- **Biodiversity Improvement**  
  ![biodiversity_chart](docs/biodiversity.png)  

- **Forest Cover Change (Heatmap)**  
  ![heatmap_chart](docs/heatmap.png)  

---

##  Working

```bash
# Clone repo
git clone https://github.com/your-username/project-prakriti.git
cd project-prakriti

# Install dependencies
pip install -r requirements.txt
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
```bash
# Run the Project
python prakriti.py

# Future Enhancements
Integrate NASA MODIS NDVI dataset for real vegetation greenness.
Use live climate APIs instead of static inputs.
Add GIS-based maps for restoration zones.
Build a community portal for citizen participation.

# Contributors
Kumar Harsh (Lead Developer & Researcher)

#  Run the Project
python prakriti.py

#Future Enhancements

 Integrate NASA MODIS NDVI dataset for real vegetation greenness.

 Use live climate APIs instead of static inputs.

 Add GIS-based maps for restoration zones.

 Build a community portal for citizen participation.

# Contributors

# Kumar Harsh (Lead Developer & Researcher)
