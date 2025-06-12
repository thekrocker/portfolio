# Aquapark Tycoon: Idle Game

> A mobile idle-arcade game where players build, manage, and grow their own waterpark empire.

---

## 🗂 Overview

- **Genre**: Idle / Arcade / Tycoon  
- **Platform**: Android  
- **Engine**: Unity 2022.3  
- **Language**: C#  
- **Tools**: Zenject (DI), UniTask, DOTween, Firebase, Addressables  

---

## 📸 Media

> *Manage water slides, ticket booths, pools, and expand your park into a full aqua-themed empire.*

[Play on Google Play Store](https://play.google.com/store/apps/details?id=games.rawbyte.waterparktycoon)

---

## 💻 What I Did

- Built the core idle loop: earnings → upgrades → unlock new zones  
- Created zone-based progression with unlock animations and level design tools  
- Developed visitor & worker **AI using a simple state machine system** (Idle, Walk, Swim, Interact, Clean, Fix) to simulate realistic guest behavior and increase production polish  
- Simulated **basic swimming and water physics** for better immersion and visual feedback  
- Used ScriptableObjects to define and balance attractions, upgrades, and costs  
- Used **Zenject** for scalable and testable architecture  
- Handled async animations, upgrades, and timed logic using **UniTask**  
- Integrated Firebase for analytics and event tracking  
- Optimized performance using pooling and reduced GC allocations  

---

## 🔧 Key Features

- ✅ Modular attraction and upgrade system  
- ✅ AI-driven visitors with swimming, walking, and idling behaviors  
- ✅ Zone unlock system with progression gates  
- ✅ Reward systems: ads, boosters, idle time bonuses  
- ✅ Save/load with a custom service layer  

---

## 🧪 Challenges & Solutions

> **Challenge**: Managing zone-specific logic and NPC behavior across large areas  
> **Solution**: Used local attraction managers and lightweight state machines to isolate behavior and improve performance.

> **Challenge**: Making pools feel dynamic without heavy physics  
> **Solution**: Simulated water interaction with position-based float/splash animation triggers and simple drag resistance.

---

## 🔬 Technical Highlights

- **Zenject** for clean dependency management and testable systems  
- **UniTask** for UI animation flow, ad timing, and reward delays  
- **ScriptableObjects** for modular balancing of attractions and upgrades  
- **AI State Machine** for controlling visitor flow and interaction  
- **Swimming system** integrated with attraction logic to boost immersion  

---

## 🧠 Lessons Learned

- A structured state machine for AI gives both clarity and control when scaling NPC behavior  
- Fake water physics can go a long way — simple systems used right can outperform complex ones visually  
- Scalable architecture with Zenject saved time in late-stage balancing and patching  
- Keeping UI and gameplay async-friendly (with UniTask) improves perceived responsiveness  
- Separating data from behavior helped us rapidly tune content during testing  

---

## 📦 Tech Stack

`Unity • C# • Zenject • UniTask • DOTween • ScriptableObjects • Firebase • Addressables • GameAnalytics`
