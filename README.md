# Open-Source-Routing-Machine


A comprehensive collection of Jupyter Notebooks demonstrating how to programmatically interact with the OSRM routing engine using Python.

This repository walks through the core OSRM services:

- **Route** — Compute optimized paths between waypoints  
- **Nearest** — Snap raw coordinates to the routable network  
- **Table** — Generate travel time matrices  
- **Match** — Align GPS traces to the road graph  
- **Trip** — Solve Traveling Salesman Problem (multi-stop optimization)  
- **Advanced Usage** — Modifying internal point limits & batching  

Each notebook is structured to be clear, consistent, and informative — ideal for learning, experimentation, or extension into production workflows.

---

## Notebooks Overview

| Notebook | Description |
|----------|-------------|
| **01_OSRM_Route_Computation_and_Analysis.ipynb** | Basics of the Route API, extracting routing metrics, and map visualization. |
| **02_OSRM_Nearest_Service_Analysis.ipynb** | Using the Nearest endpoint to snap GPS data to the road network. |
| **03_OSRM_Table_Service_Analysis.ipynb** | Generating and interpreting duration matrices between locations. |
| **04_OSRM_Match_Service_Analysis.ipynb** | Map matching of raw GPS traces to the road network. |
| **05_OSRM_Trip_Service_Analysis.ipynb** | Solving multi-stop optimization using the Trip service. |

---

## Key Features

✔ **Structured workflow examples** — each notebook follows a clean, analytical approach for clarity.  
✔ **Interactive maps** — using `folium` for live route and point visualization.  
✔ **Reproducible code** — ready to run with minimal setup.  
✔ **Real GPS data handling** — GPX parsing and matching with timestamp support.  
✔ **Configurable parameters** — demonstrating optional OSRM settings like radiuses, roundtrips, and constraints.  

---

## Using Docker with OSRM
Make sure to have Docker installed 

Open Docker

And to make sure its running

Get inside yout Terminal and run
```bash
docker version
```
---

Download OpenStreetMap extracts for example from [ Geofabrik](https://download.geofabrik.de/)

Download the pbf file
Save it inside a folder, get into that directory of that particular file inside the terminal

```bash
docker run -t -v D:/OSRM_Data/data:/data ghcr.io/project-osrm/osrm-backend osrm-extract -p /opt/car.lua /data/bremen-latest.osm.pbf
```
My saved the downloaded file inside a folder called /data

NOTE:

to change  "bremen-latest.osm.pbf" to your selected/downloaded region name

NOTE:

Extraction may take significant time depending on file size.

---
## Folder Structure

```text
Project Root
│
├── data
│   └── bremen-latest.osm.pbf
├── Open-source-routing-machine (This repo)
│       ├── data
│       ├── notebooks
│       ├── .gitignore
│       ├── README.md
│       └── requirements.txt
```


---
### Partition the Data
```bash
docker run -t -v <project_root>:/data ghcr.io/project-osrm/osrm-backend osrm-partition /data/bremen-latest.osrm
```

---

### Customize the Graph
```bash
docker run -t -v <project_root>:/data ghcr.io/project-osrm/osrm-backend osrm-customize /data/bremen-latest.osrm
```
OSRM generates multiple files sharing the same base name
The .osrm path acts as a base prefix, not a standalone file.

---

### Start the Routing Server
```bash
docker run -t -i -p 5000:5000 -v "<project_root>:/data" ghcr.io/project-osrm/osrm-backend osrm-routed --algorithm mld /data/bremen-latest.osrm
```

Once running, the routing engine will be available at: http://localhost:5000

---
## Request Against the Demo Server

Now run the below code in a new terminal while getting inside the same directory
The coordinates that I used here are for Bremen. Please make sure to change them for your selected region before running it.

```bash
curl.exe http://localhost:5000/route/v1/driving/8.801693,53.079296;8.807281,53.075819?steps=true&alternatives=true
```
The above code will start the local host


---
# Running the Notebooks Locally

After setting up the OSRM backend with Docker, the next step is to run the Python notebooks included in this repository.

## Clone or Download This Repository

Or download it as a ZIP file from GitHub and extract it locally.

---
## Open the Project in VS Code

Open Visual Studio Code
Click on File → Open Folder
Select the cloned/extracted project directory

Make sure you have the following VS Code extensions installed:

✔ Python (by Microsoft)

✔ Jupyter (by Microsoft)

---
## Create or Select a Python Environment

Before running the notebooks, ensure you are using:
Python version 3.8 or higher

Inside your Terminal:
You can verify your Python version by running:
``` bash
python --version
```

If needed, create a virtual environment:
```bash
python -m venv venv
```
---

## Select the Interpreter in VS Code

Inside VS Code:
Press Ctrl + Shift + P

Search for Python: Select Interpreter

Choose the virtual environment you created

Make sure it shows Python ≥ 3.8

For Jupyter notebooks:
Click the Kernel selector (top right) in the notebook
Select the correct Python environment

---
## Start Running the Notebooks

Now you can begin executing the notebooks in order:

01_OSRM_Route_Computation_and_Analysis.ipynb

02_OSRM_Nearest_Service_Analysis.ipynb

03_OSRM_Table_Service_Analysis.ipynb

04_OSRM_Match_Service_Analysis.ipynb

05_OSRM_Trip_Service_Analysis.ipynb

---

### Important Notes
- Make sure the OSRM Docker server is running on port 5000 before executing service requests.
- Verify that your .osm.pbf file has already been processed.
- Ensure Docker is active and accessible.
- Make sure that the .pbf file and the downloaded repo are under the same folder

---

This repository was created as a beginner-friendly, hands-on guide to understanding and working with the Open Source Routing Machine (OSRM) using Python.
The goal of this project is to:
- Break down each OSRM service into clear, structured notebooks
- Provide practical, real-world examples using actual GPS traces
- Explain both the theory and implementation step by step
- Make routing concepts accessible to developers at any level

Each notebook builds on the previous one, forming a progressive learning path — from basic route computation to advanced services like Match, Trip (TSP), and modifying service limitations.

---

## Who Is This For?

This repository is ideal for:
- Developers new to OSRM
- Students learning routing algorithms
- Engineers working with GPS trajectory data
- Anyone interested in map matching and route optimization








