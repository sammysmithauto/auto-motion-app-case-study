# Auto-Motion: Motion Media Workflow Automation

## 🚀 Overview

The **Auto-Motion App** (developed from the **IKEA MM Script App** prototype) is a cross-platform desktop utility built to standardize motion media workflows. By bridging high-fidelity UX with a functional automation backend, the tool eliminates repetitive manual setup and enforces global naming and metadata conventions across production teams.

* 
**Role:** Strategic Lead & Post-Production Script Developer.


* 
**Impact:** Developed a unified "Design-to-Code" pipeline, transitioning a Figma prototype into a functional Electron/React/Python application.


* 
**Portfolio:** [Project Showcase](https://vimeo.com/1106703061?fl=pl&fe=sh).



---

## ⚙️ Technical Architecture: The React-Python Bridge

The application utilizes a modular architecture to handle complex media processing while maintaining a high-performance UI.

### 🔗 IPC & CLI Integration

A key technical achievement was engineering the bridge between the **React** frontend and the **Python** automation engine using Electron’s **IPC (Inter-Process Communication)**.

```javascript
// Electron IPC Handler for Python Script Spawning
ipcMain.handle("listProjectTemplates", async () => {
  return new Promise((resolve, reject) => {
    const helperPath = path.resolve(app.getAppPath(), '../backend/src/scripts/utilities/project_templates_cli.py');
    const py = spawn("python3", [helperPath, "--list", "--non-interactive"]);
    let out = "", err = "";
    py.stdout.on("data", (c) => (out += c));
    py.stderr.on("data", (c) => (err += c));
    py.on("close", (code) => {
      if (code === 0) {
        try {
          resolve(JSON.parse(out)); // Return structured JSON to Frontend
        } catch (e) {
          reject(e);
        }
      } else {
        reject(new Error(err || `exit code ${code}`));
      }
    });
  });
});

```

* **Process Spawning:** Utilizes `child_process.spawn` to execute Python CLI wrappers in non-interactive modes.
* **Asynchronous Handling:** IPC handlers manage asynchronous promises to return structured JSON data from the Python backend to the frontend state.
* **Security:** Implements `contextIsolation` and `sandbox: true` within Electron’s web preferences to secure the bridge between the renderer and native OS resources.

---

## 💎 Core Functionalities

The app serves as a centralized hub for technical directors and editors to manage the production lifecycle.

### 1. Automated Project Templating

* **Standardization:** Generates structured directory trees and DaVinci Resolve project files instantly based on enterprise templates.
* 
**Naming Conventions:** Enforces strict naming logic to ensure asset traceability across **Censhare** and **IDAM** systems.



### 2. Metadata & Scripting Engine

* **Bulk Management:** Tools for importing, exporting, and resetting clip attributes via CSV and JSON configuration files.
* **Automated Assembly:** The "Append Clips" tool uses metadata to automatically generate timestamped timelines and rough cuts, removing manual assembly from the edit process.

### 3. Native Desktop Integration

* **System Tray Utility:** Built a resident system tray menu for quick access to specific production pages and tools.
* 
**Cross-Platform Performance:** Developed and tested for macOS and Windows, handling native path resolutions for enterprise storage solutions.



---

## 🏛️ Strategic Development Phases

### Phase 1: Prototype (IKEA MM Script App)

Initial discovery focused on proving the business case through UI/UX research.

* 
**Systemic Design:** Integrated the **IKEA Skapa** design system into high-fidelity Figma prototypes to validate user flows for project initialization.


* 
**Requirements Gathering:** Conducted **WCAG accessibility** research and stakeholder demos to define the automation roadmap.



### Phase 2: Pipeline Engineering (Auto-Motion App)

Transitioned the prototype into a production-ready system with deep API integrations.

* 
**DaVinci Resolve API:** Built deep integrations with the Resolve Studio API to drive bin organization and rendering workflows.


* 
**Scalability:** Researched and integrated with **Beräkna** render-farm solutions for high-volume, remote media processing.



---

## 🛠️ Technical Skillset

* 
**Languages:** Python (Automation, API Logic), JavaScript/TypeScript (React, Electron).


* 
**Production APIs:** DaVinci Resolve Python API, Beräkna Render Farm API.


* 
**Tools:** Figma (Prototyping), GitHub (Version Control), Jira/Confluence (Roadmapping & Documentation).


* 
**Design Systems:** IKEA Skapa.



---

**Footnote:** *This repository functions as a technical case study. The core codebase and internal IKEA Skapa components are proprietary and not included for public distribution.*
