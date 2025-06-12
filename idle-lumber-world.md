# Idle Lumber World

> An idle-arcade simulation game where players chop trees, build structures, and expand their lumber empire step by step.

---

## 🗂 Overview

- **Genre**: Idle / Arcade / Simulation  
- **Platform**: Android  
- **Engine**: Unity 2022.3  
- **Language**: C#  
- **Tools**: Zenject, DOTween, Addressables, UniTask  

[Play on Google Play Store](https://play.google.com/store/apps/details?id=games.rawbyte.idlelumberworld)

---

## 💻 What I Did

- Designed and developed the **entire gameplay system** from scratch, following the idle arcade model  
- Created a **modular unlock system**, allowing new areas, machines, and zones to open progressively based on player actions  
- Built a flexible **interaction system** that supports player-object and NPC interactions (gathering, building, upgrading)  
- Handled **large-scale environment interactions** using optimized crowd tree handling and **mesh combining techniques** to reduce draw calls  
- Implemented an **advanced save/load system** capable of saving upgrades, stateful world objects, and currency  
- Used **ScriptableObjects** for managing upgrades, area data, and unlock rules  
- Focused heavily on **mobile performance**, especially around large scenes and mass object updates  

---

## 🔧 Key Features

- ✅ Modular unlock and area progression system  
- ✅ Tree-cutting and structure-building loop  
- ✅ Interaction system for tools, objects, and unlockables  
- ✅ Optimized tree crowd system using mesh combination and pooling  
- ✅ Advanced save/load with upgrade persistence  
- ✅ UI feedback integrated with player progress and world state  

---

## 🧪 Challenges & Solutions

> **Challenge**: Rendering and interacting with hundreds of trees in a single scene  
> **Solution**: Used mesh combining, pooled objects, and group batching strategies to minimize overhead on mobile.

> **Challenge**: Designing a scalable save system to track upgrades and world state  
> **Solution**: Created a custom save architecture with per-zone and per-feature data separation, reducing load/save time and supporting future expansion.

---

## 🔬 Technical Highlights

- Modular system design following SRP and clean architecture principles  
- Save system built around data-driven serialization, supporting both versioning and partial restore  
- Interaction logic abstracted via interfaces, allowing future reuse (NPCs, zones, tools)  
- MeshCombiner utility to group nearby trees and reduce CPU/GPU load dynamically  
- Addressables used for dynamic zone loading and content separation  

---

## 🧠 Lessons Learned

- Clean, modular architecture is essential when building systems with expanding complexity  
- Mesh combination can drastically improve mobile performance but needs careful planning for interactivity  
- Advanced save systems should be extensible from the start to avoid refactoring during feature growth  
- Building scalable interaction systems early speeds up future feature development and designer iteration  

---

## 📦 Tech Stack

`Unity • C# • Zenject • UniTask • DOTween • ScriptableObjects • Addressables • Mesh Combining • Object Pooling`
