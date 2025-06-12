# Fashion Challenge: Catwalk Run

> A fast-paced hybrid casual game where players style their model, walk the runway, and compete in fashion challenges.

---

## 🗂 Overview

- **Genre**: Hybrid Casual / Dress-up / Runner  
- **Platform**: Android  
- **Engine**: Unity 2022.3  
- **Language**: C#  
- **Tools**: Zenject, UniTask, Firebase Remote Config, DOTween, Addressables, GameAnalytics

[Play on Crazy Games](https://www.crazygames.com/tr/oyun/fashion-challenge-catwalk-run)

---

## 📸 Media

<div style="display: flex; gap: 12px; flex-wrap: wrap; justify-content: flex-start;">
  <img src="https://play-lh.googleusercontent.com/oOGxMu-Kqfin4k6Cn-auiYRiy9LY9bQ3mE60kPAVVI8hqa7F-aQMb4QQkZGXUq-VKAQy=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://play-lh.googleusercontent.com/_nB549vV4g10xRMEjPSRKJ991r8h6bL6zYKOgLqzVMZUycIrs-52nEkrMp4CmL4SOMI=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
  <img src="https://play-lh.googleusercontent.com/fNMHWQtvP5wfu4K_1xLIyRohBA_wrD7WzT6Ybrl5pHFuZ02vJ0dsW7zLL5PjjhwQgytx=w2560-h1440-rw" style="width: 20%;" alt="Gameplay Screenshot">
</div>

> *Style your model, hit the runway, and climb the leaderboard in this live-operated fashion challenge.*

---

## 💻 What I Did

- Developed a LiveOps-ready backend integration with **Firebase Remote Config**, allowing us to change reward values, event conditions, and pricing without client updates  
- Built a dynamic **IAP shop system** with configurable offers (bundles, timed packs, starter deals), linked to Adjust and revenue events  
- Created a modular **animation system** using polymorphism and script-driven triggers for camera moves, runway poses, and end-of-level sequences  
- Implemented **Firebase Realtime Leaderboards**, supporting global and segmented event rankings  
- Managed timed campaigns like "Event of the Week" and "Best Outfit Challenge" through data-driven configs  
- Used **Zenject** to structure the project for maintainability across gameplay, UI, and shop logic  
- Applied **UniTask** to simplify asynchronous UI flows and reward delivery (ad watching, IAPs, daily rewards)

---

## 🔧 Key Features

- ✅ LiveOps support via Remote Config for tuning, offers, and events  
- ✅ Dynamic IAP system with timed bundles and adjustable pricing  
- ✅ Leaderboard integration (Firebase) with event-based reset logic  
- ✅ Animation system built with interfaces and behavior polymorphism  
- ✅ Modular save/load and economy system using service-based structure  

---

## 🧪 Challenges & Solutions

> **Challenge**: Managing event content and balancing without new builds  
> **Solution**: Used Firebase Remote Config to drive event reward values, outfit availability, and IAP visibility from the backend.

> **Challenge**: Scaling animation logic across levels with different runway styles  
> **Solution**: Built an animation controller base interface, then derived classes for each level style — making it easy to reuse logic and inject behavior dynamically.

---

## 🔬 Technical Highlights

- **Firebase Remote Config** for real-time tuning of economy and features  
- **IAP Shop**: Configurable offer system driven by server toggles and timers  
- **Firebase Leaderboard** with async ranking fetch + update  
- **Animation Layer System** for pose transitions and performance-based feedback  
- **Zenject** used across gameplay, economy, and LiveOps subsystems  
- **UniTask** for all async flows (ads, IAP, reward delays, transitions)

---

## 🧠 Lessons Learned

- LiveOps is not just about server config — architecture must be built for flexibility from day one  
- Structuring animation logic with polymorphism allowed us to scale new level types quickly  
- Remote Config gave us a huge boost in iteration speed, especially during early monetization tests  
- Building backend-driven content systems (leaderboards, events, IAP) taught me to think from both player and ops perspectives  

---

## 📦 Tech Stack

`Unity • C# • Zenject • UniTask • Firebase Remote Config • Firebase Leaderboard • Adjust • DOTween • ScriptableObjects • Addressables • GameAnalytics`
