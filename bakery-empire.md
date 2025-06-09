# 🎮 Project Title: *Idle Bakery Empire*

> A casual idle game where players bake, upgrade, and automate a growing bakery empire.

---

## 🗂 Overview

- **Genre**: Idle / Arcade
- **Platform**: Android / iOS
- **Engine**: Unity 2022.3.45f
- **Tools**: C#, Zenject, DOTween, ScriptableObjects, Firebase, Adjust, GameAnalytics

---

## 📸 Media

<img src="https://img001.prntscr.com/file/img001/b-PuZH41QKOFu-zU7pzb2A.png" width="600" alt="Gameplay Screenshot">

> *(You can watch the trailer below.)*

<a href="https://www.youtube.com/watch?v=zm9DI4lpowE" target="_blank">
  <img src="https://img.youtube.com/vi/zm9DI4lpowE/hqdefault.jpg" width="300" alt="Watch the Gameplay Trailer" style="position: relative;">
</a>


---

## 💻 What I Did

- Built entire idle production and upgrade loop
- Implemented offline income logic using device time
- Integrated Zenject for scalable DI architecture
- Optimized performance for low-end Android devices
- Wrote reusable systems using ScriptableObjects (UpgradeData, ProductData)
- Designed a configurable Daily Reward System.
- Developed a dynamic in-game shop system driven by JSON/config files
- Handled IAP and virtual currency logic using a clean service-based architecture
- Created modular shop items (skins, boosts, bundles) using ScriptableObjects
- Designed a flexible quest system with daily/weekly objectives using ScriptableObject definitions
---

## 🔧 Key Features

- ✅ Modular idle factory production system
- ✅ Offline earnings and reward boost mechanics
- ✅ Daily rewards and ad-based monetization
- ✅ Save/Load system with ISaveService interface
- ✅ Shop & Inventory UI with dynamic buttons

---

## 🧪 Challenges & Solutions

> **Problem**: Framerate dropped significantly when product count increased.
> **Solution**: Combined meshes, Used object pooling, reduced GC allocations, and simplified UI refresh logic.

---

## 📊 Metrics & Impact

- 🚀 Over 50,000 downloads on Store

---

## 🔬 Technical Deep Dive

- **Zenject Setup**:
    - SceneContext + ProjectContext used for layered injection
    - Signals used for UI ↔ Game events decoupling

- **ScriptableObject Usage**:
    - `ProductData`, `UpgradeLevel`, and `AdSettings` are all data-driven

- **Offline Calculation**:
    - Device time used to calculate elapsed production and earnings
    - Handles tampering by tracking last saved time vs current time

---

## 🧪 Code Samples
-- To be added later --

---

## 🧠 Lessons Learned

> I learned to separate game state from view logic, design feature gates for LiveOps, and implement decoupled systems with proper SOLID architecture.

---

## 📦 Tech Stack

`Unity • C# • Zenject • DOTween • ScriptableObjects • Firebase • Addressables`

---
