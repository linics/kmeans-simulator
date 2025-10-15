# AI Agent Specification — K-Means Interactive Lesson

## 📘 Project Overview
Goal:  
Develop a **single-file interactive HTML lesson** that teaches **K-Means clustering**.  
This project is intended for **middle-school or early university AI education**, combining bilingual (Chinese + English) explanations with live visualization and small interactive quizzes.

The system must run **offline in a browser** (no external libraries or CDN), and be **fully self-contained** (`index.html` only).

---

## 🧩 Project Objectives
1. Introduce the concept and algorithm of K-Means (steps, intuition, and limitations).  
2. Provide an **interactive SVG visualization** of the clustering process.  
3. Allow users to adjust parameters (k, distance metric, dataset type, iterations).  
4. Display real-time metrics such as **SSE (Sum of Squared Errors)** and **Silhouette Score**.  
5. Include a short bilingual quiz section for review and feedback.  
6. Support export of the visualization to PNG.  
7. Ensure bilingual UI and textual explanations (Chinese + English).

---

## ⚙️ Technical Requirements
- **File count**: Only one file — `index.html`
- **Languages**: Pure HTML + CSS + Vanilla JavaScript
- **Libraries**: ❌ None (no CDN / external scripts)
- **Runtime**: Must run offline in any modern browser
- **Structure**: Split into modular JS functions (RNG, Dataset, KMeans, Renderer, Metrics, UI)
- **Graphics**: Use SVG for points, centroids, and optional Voronoi visualization
- **Style**: Clean, responsive layout with clear color contrast
- **Accessibility**: Provide `aria-label`s and visible focus states
- **Language**: All user-facing text bilingual (Chinese + English)

---

## 🧱 UI Layout Specification

### Top Bar
Buttons:
- `Reset 重置`
- `Run 运行`
- `Step 单步`
- `Pause 暂停`
- `Download PNG 导出图片`

Also show:
- Iteration count
- SSE (Sum of Squared Errors)
- Silhouette Score (average)

### Left Panel — Controls
- Dataset type: `Blobs`, `Concentric Circles`, `Moons`, `Grid`, `Custom`
- Parameters:
  - k (clusters)
  - Initialization: `Random` | `k-means++`
  - Distance: `Euclidean` | `Manhattan`
  - Max iterations
  - Random seed
  - Point count
  - Noise ratio
- Options (checkboxes):
  - Show Voronoi
  - Show Trails
  - Show Labels
  - Show Heatmap

### Right Panel — Tabs
1. **Concept 概念** — bilingual explanation of algorithm & intuition  
2. **Metrics 指标** — definition and meaning of SSE and Silhouette  
3. **Quiz 小测验** — 4 multiple-choice questions with instant feedback  
4. **When It Fails 何时失效** — examples of non-convex / noisy datasets and short textual notes  

### Footer
- License, author name, creation date

---

## 🧠 Algorithm Requirements

### Initialization
- Random k points or k-means++ (choose based on user selection)

### Iteration Loop
1. **E-step**: assign each point to the nearest centroid  
2. **M-step**: update centroids as the mean of assigned points  
3. Stop when:
   - max iterations reached, or
   - centroid movement < epsilon

### Metrics
- **SSE**: total within-cluster squared distance  
- **Silhouette (simplified)**: (b - a) / max(a, b), using up to 300 samples for performance

### Empty Cluster Handling
If a cluster becomes empty, reinitialize its centroid using the farthest point from current centroids.

---

## 🧩 Dataset Generator
- Implement deterministic RNG (e.g., `mulberry32(seed)`)
- Provide `generateBlobs`, `generateCircles`, `generateMoons`, `generateGrid`, and `generateCustom` functions
- Add noise according to slider ratio (0–0.3)

---

## 🧠 Bilingual Content Example

### Concept Tab
- What is K-Means? 什么是 K-Means？
  > Partition n points into k clusters by minimizing within-cluster variance.  
  > 将样本划分为 k 个簇，最小化簇内方差。

- Steps 步骤:
  1. Initialize centroids (随机或 k-means++)  
  2. Assign each point  
  3. Update means  
  4. Repeat until convergence  

- When to use 适用场景: roughly spherical clusters  
- Limitations 局限: sensitive to init/outliers, assumes convex clusters  

### Quiz Tab
- 4 questions, each with options, bilingual feedback  
- “Retake 重新作答” button after completion

---

## 🪄 Phased Execution Plan

To avoid timeout and partial generation, **Codex should execute in three stages**:

### **Phase 1 — Layout & Static Structure**
Goal:  
Build page layout (HTML + CSS), including panels, buttons, and bilingual labels, but **no JS logic yet**.

Deliverable:  
`index.html` with static structure, ready to attach JS.

---

### **Phase 2 — Algorithm & Visualization**
Goal:  
Implement K-Means logic, SVG rendering, centroid updates, dataset generation, and metrics calculation.

Deliverable:  
Same `index.html` file, now interactive with working clustering animation.

---

### **Phase 3 — Enhancements & Quiz**
Goal:  
Add quiz tab, export-to-PNG, silhouette metric, keyboard shortcuts, and small visual polish.

Deliverable:  
Final version of `index.html` ready for offline use.

---

## 🧩 Interaction Commands (for developer)
- “Execute Phase 1” → builds layout  
- “Execute Phase 2” → adds logic  
- “Execute Phase 3” → final polish  
- “Refine UI wording” → rewrite bilingual labels  
- “Explain K-Means conceptually” → print educational summary  

---

## ✅ Completion Checklist
- [ ] Single file only (`index.html`)
- [ ] All buttons functional
- [ ] Works offline
- [ ] SSE decreases over iterations
- [ ] Silhouette score updates
- [ ] Dataset switchable
- [ ] Export PNG works
- [ ] Quiz functional
- [ ] Bilingual texts visible
- [ ] Responsive layout (desktop priority)

---

**End of agent.md**
