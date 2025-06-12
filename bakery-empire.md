# 🎮 Idle Bakery Empire

> A mobile idle game where players bake, upgrade, and grow their automated bakery empire.

---

## 🗂 Overview

- **Genre**: Idle / Arcade
- **Platform**: Android / iOS
- **Engine**: Unity 2022.3
- **Language**: C#
- **Tools**: Zenject, DOTween, UniTask, Firebase, Adjust, GameAnalytics

[Play on Google Play Store](https://play.google.com/store/apps/details?id=games.rawbyte.bakeryidle&hl=en)

---

## 📸 Media

<img src="https://img001.prntscr.com/file/img001/b-PuZH41QKOFu-zU7pzb2A.png" width="600" alt="Gameplay Screenshot">

> *Gameplay showing the upgradeable bakery and production flow.*

<a href="https://www.youtube.com/watch?v=zm9DI4lpowE" target="_blank">
  <img src="https://img.youtube.com/vi/zm9DI4lpowE/hqdefault.jpg" width="300" alt="Watch the Gameplay Trailer">
</a>

---

## 💻 What I Did

- Built the full idle production and upgrade system
- Added offline income and anti-cheat time logic
- Designed daily rewards and quest systems
- Created a dynamic in-game shop with ScriptableObjects
- Integrated Zenject for modular architecture
- Optimized performance for low-end mobile devices
- Handled IAP and reward systems with service-based structure

---

## 🔧 Key Features

- ✅ Modular idle system with product upgrades
- ✅ Offline earnings & reward boosts
- ✅ Daily rewards and ad monetization
- ✅ Save/load using `ISaveService`
- ✅ JSON-configurable in-game shop

---

## 🧪 Challenges & Solutions

> **Problem**: Lag on devices with many products.  
> **Solution**: Used object pooling, mesh combining, and reduced GC spikes.

---

## 📊 Metrics & Impact

- 🚀 50,000+ downloads
- 🔧 LiveOps-ready economy tuning via remote configs

---

## 🔬 Technical Highlights

- Zenject used with SceneContext + ProjectContext
- Async operations managed using **UniTask**
- Production and upgrade logic driven by ScriptableObjects
- Offline time calculation protected against device tampering

---

## 🧠 Lessons Learned

- Learned how to keep idle systems modular and scalable
- Offline earnings require careful time handling and fallback logic
- Mobile optimization is all about batching, pooling, and memory control
- Small UX details (like reward feedback) directly affect retention
- Clean content pipelines save tons of time as the game grows

---

## 📦 Tech Stack

`Unity • C# • Zenject • UniTask • DOTween • ScriptableObjects • Firebase • Adjust • GameAnalytics • Addressables`
