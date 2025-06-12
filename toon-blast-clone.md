# Toon Blast Clone – Peak Case Study

> A fast-paced match-2 puzzle game built in 5 days for a case study inspired by *Toon Blast*. Includes a full editor, custom match logic, and classic modifiers like rockets, balloons, and ducks.

---

## 🗂 Overview

- **Genre**: Puzzle / Match-2 / Arcade  
- **Platform**: PC / Mobile (Unity)  
- **Engine**: Unity  
- **Language**: C#  
- **Case Study**: Designed and delivered as part of a *Peak Games* technical challenge

---

## 💻 What I Did

- Created the **entire game from scratch**, including all core systems and visuals in under a week  
- Implemented an **improved flood-fill algorithm** to detect connected same-color neighbors  
- Built a responsive **Level Editor** that allows fast drag-and-drop piece setup and visual board creation  
- Developed a **Quest System** with required goals and a **limited move system** to challenge players  
- Used **Object Pooling** to spawn and reuse elements efficiently during gameplay  
- Implemented a **Responsive Board System** that adjusts camera and layout based on board dimensions  
- Created various board **Modifiers**:
  - **Rocket**: Destroys rows or columns, can chain with other rockets  
  - **Balloon**: Pops when nearby matches occur  
  - **Duck**: Must be dropped to the bottom to be matched (not destroyable by rockets unless flagged)

- Developed **Shuffle logic** for deadlock handling or manual reshuffling

---

## 🔧 Key Features

- ✅ Flood-fill neighbor detection algorithm  
- ✅ Level Editor with real-time piece placement and preview  
- ✅ Match mechanics and combo triggers  
- ✅ Reward logic with extensible modifier conditions  
- ✅ Responsive camera and board scaling  
- ✅ Modifier chaining (rockets triggering each other)  
- ✅ Duck, Balloon, and Shuffle mechanics  

---

## 🧪 Challenges & Solutions

> **Challenge**: Efficiently detecting and tracking adjacent matches with color rules  
> **Solution**: Implemented a recursive flood-fill approach optimized for performance and clarity

> **Challenge**: Dynamic board layout on different screen sizes  
> **Solution**: Created a camera controller and board frame scaler that adapt to board dimensions with margin safety

---

## 🔬 Technical Highlights

- **Flood-Fill Algorithm** for match detection  
- **2D Array-based Board Grid** with pooled objects  
- **Custom Editor Tool** for level building using Resources folder auto-loading  
- **Object Pooling System** to avoid runtime instantiation costs  
- **Modifier Architecture** built around interfaces (`IUntouchable`, `IModifierTriggerable`) for easy expansion  
- **Responsive Board** system: adjusts both visual frame and orthographic size automatically  

---

## 🧠 Lessons Learned

- Algorithm performance matters — flood-fill and search operations must be lean  
- Rapid prototyping benefits massively from having good editor tooling early on  
- Clean modifier design using interfaces made chaining and new behavior integration much easier  
- UI/UX polish for match feedback (collapse, reward triggers) is key to a satisfying puzzle feel  
- Given more time, I would replace PlayerPrefs with JSON-based saving and integrate Firebase for LiveOps potential

---

## 📦 Tech Stack

`Unity • C# • Flood-Fill Algorithm • Custom Level Editor • Object Pooling • 2D Grid System • Modifier Pattern • Responsive Design`
