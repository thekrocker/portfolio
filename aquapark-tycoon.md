# Aquapark Tycoon: Idle Game

> A mobile idle-arcade game where players build, manage, and grow their own waterpark empire.

---

## 🗂 Overview

- **Genre**: Idle / Arcade / Tycoon  
- **Platform**: Android  
- **Engine**: Unity 2022.3  
- **Language**: C#  
- **Tools**: Zenject (DI), UniTask, DOTween, Firebase, Addressables  

[Play on Google Play Store](https://play.google.com/store/apps/details?id=games.rawbyte.waterparktycoon)

---

## 📸 Media

> *Manage water slides, ticket booths, pools, and expand your park into a full aqua-themed empire.*

<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://play-lh.googleusercontent.com/496F_Gvcc8mlndYht_zhECvAzq6JBcXTYYW-HgCapW-Q6JywheyoowAHMZ9xj8xv2KA=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://play-lh.googleusercontent.com/9pTnwKEcIdiWrVYy5D8K9AM9N93c5q3jppFnj406nyDXwj5OEBEzYLv6ZxglEXk8Fa1o=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://play-lh.googleusercontent.com/miKUrHeTIlW1DzW9JEv101GB3DaDD39zB1HzCJ6-qXGjq3VmemO1x-ddh0LL18nR8Q=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
</div>


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
