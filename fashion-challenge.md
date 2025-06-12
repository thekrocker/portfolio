# Fashion Challenge: Catwalk Run

> A fast-paced hybrid casual game where players style their model, walk the runway, and compete in fashion challenges.

---

## 🗂 Overview

- **Genre**: Hybrid Casual / Dress-up / Runner  
- **Platform**: Android  
- **Engine**: Unity 2022.3  
- **Language**: C#  
- **Tools**: Zenject, UniTask, Firebase Remote Config, DOTween, Addressables, GameAnalytics  

---

## 📸 Media

> *Style your model, hit the runway, and climb the leaderboard in this live-operated fashion challenge.*

[Play on Google Play Store](https://play.google.com/store/apps/details?id=com.TriflesGames.FashionChallenge)

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
