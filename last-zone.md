# Last Zone – Idle Survival

> A post-apocalyptic idle survival game where players rebuild civilization, manage survivors, loot for gear, and fight in a turn-based PvP arena. Inspired by titles like *Idle Outpost* and *Idle Zombie Survival*.

[Play on Google Play Store](https://play.google.com/store/apps/details?id=com.paperpigeon.populationoneidle)

---

## 🗂 Overview

- **Genre**: Idle / Survival / Management  
- **Platform**: Android  
- **Engine**: Unity 2022.3  
- **Language**: C#  
- **Monetization**: IAP, Rewarded Ads, Ad Spins  
- **Architecture**: Zenject, UniTask, Remote Config, ScriptableObjects  

---

## 📸 Media

<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://play-lh.googleusercontent.com/jtu4OrV_iY1TB2Bkhv1kiFjwG7hkb1ZOUhLyr4tLWqM-DbY7KN50ji9WIfLqVjV9AA=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://i.postimg.cc/8JdLmFGH/Ekran-g-r-nt-s-2025-06-12-135135.png" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://i.postimg.cc/8JghvR2c/Ekran-g-r-nt-s-2025-06-12-135212.png" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://postimg.cc/Lq1thC0G" target="_blank"><img src="https://i.postimg.cc/Lq1thC0G/Ekran-g-r-nt-s-2025-06-12-135351.png" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://i.postimg.cc/VJT9fQ4j/Ekran-g-r-nt-s-2025-06-12-135410.png" style="width: 20%;" alt="Gameplay Screenshot">
</div>

---

## 💻 What I Did

- Built and maintained **all core systems** from the ground up using a **modular, service-based architecture**  
- Developed **multi-mode gameplay**, including:
  - **Base Management**: Survivor handling, building upgrades, idle resource generation  
  - **Loot Mini-Game**: Manual scavenging for supplies and inventory gear  
  - **Turn-Based PvP Arena**: Strategic combat system with skills, items, and energy mechanics  

- Designed a **robust LiveOps framework** including:
  - Firebase **Remote Config** for balancing, offer visibility, and global toggles  
  - **Daily rewards**, **spin wheel**, **timed offers**, and **rewarded ads** (multi-channel entry points)  
  - **Event campaign support** via external config for scalable updates  

- Implemented a **layered save/load system** that supports local and cloud sync  
- Created advanced **upgrade and progression systems** for characters, items, and buildings  
- Integrated a **modular inventory system** with loot quality, rarity, and sorting/filtering  
- Developed a fully decoupled **UI system** with async state management using **UniTask**  
- Ensured high performance and low GC allocation with **object pooling**, lightweight signals, and **SRP-friendly UI rendering**  

---

## 🔧 Key Features

- ✅ Multi-phase gameplay: idle base + looting + turn-based combat  
- ✅ Modular upgrade systems: survivors, facilities, and gear  
- ✅ Inventory system with rarity, stats, equippables  
- ✅ Full LiveOps support: daily login, spin, ad rewards, remote events  
- ✅ Firebase Remote Config for dynamic tuning and Live content  
- ✅ Turn-based PvP system with ability cooldowns and strategy layer  
- ✅ Custom save system (versioned, layered, cloud-ready)

---

## 🧪 Challenges & Solutions

> **Challenge**: Supporting multi-mode gameplay (idle + action + PvP) without bloating core systems  
> **Solution**: Used a feature-module architecture with Zenject signal separation and individual service layers for each game mode.

> **Challenge**: Live tuning of rewards, events, and feature rollouts  
> **Solution**: Integrated Firebase Remote Config with tag-based toggling and cache-safe versioning. Supported rollout fallback and value validation.

> **Challenge**: Complex inventory and upgrade logic with varying item types  
> **Solution**: Used abstracted item types, runtime ScriptableObject resolution, and generic upgrade interfaces to support future content.

---

## 🔬 Technical Highlights

- **Architecture**: Domain-driven, service-based system using Zenject for lifetime scope management  
- **LiveOps Tools**: RemoteConfig service wrapper, event flagging, timed offer visibility  
- **Async Handling**: All flows (UI, rewards, transitions) use **UniTask** with cancellation tokens  
- **UI System**: Window stack + async UI service + context-driven view updates  
- **Inventory System**: Modular gear framework, stat modifiers, equip/unequip, rarity colors, and save integration  
- **Arena Mode**: Turn-based system with cooldowns, energy control, and runtime skill modifiers  
- **Optimization**: Extensive use of pooling, view virtualization, and pre-allocated containers for mobile performance  

---

## 🧠 Lessons Learned

- **Multi-loop gameplay** requires clear separation of systems and flexible routing — core state management must remain minimal and high-level  
- **LiveOps infrastructure** is essential even for idle games — reward pacing, economy balance, and monetization all benefit from backend config  
- **Scalable inventory and upgrade systems** benefit immensely from interface-driven design  
- **Turn-based combat** design demands testable logic and ability for extension without rewriting rules  
- Writing clean code isn't enough — writing adaptable, maintainable code is critical in LiveOps-driven games

---

## 📦 Tech Stack

`Unity • C# • Zenject • UniTask • ScriptableObjects • Firebase Remote Config • Firebase Analytics • Rewarded Ads • IAP • Addressables • Custom Save System • Turn-Based Combat Engine`
