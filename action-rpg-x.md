# ⚔️ Action RPG X – GAS

> A third-person action RPG inspired by *God of War*, built almost entirely in C++ using Unreal Engine’s Gameplay Ability System (GAS).

---

## 🗂 Overview

- **Genre**: Action RPG
- **Platform**: PC
- **Engine**: Unreal Engine 5.5
- **Language**: C++ (99%)
- **Core System**: Gameplay Ability System (GAS)

---

## 📸 Media

<video width="640" controls>
  <source src="_media/actionrpg/showcase-1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
> *Showcase of combat, abilities, and animation syncing using GAS.*

---

## 💻 What I Did

- Built all core gameplay using GAS: light/heavy attacks, stamina, blocking, dashing, and effects.
- Wrote custom `AbilitySystemComponent` and attribute sets in C++.
- Created a combo system using animation montages and section transitions.
- Used tags to manage input, cooldowns, and gameplay states.
- Connected gameplay to UI using attribute replication and events.
- Designed upper-body animation blending to allow attacks during movement.
- Synced damage, VFX, and sounds with animation using notifies.

---

## 🔧 Key Features

- ✅ Full C++ GAS setup
- ✅ Melee combo system
- ✅ Attributes: Health, Stamina, Damage
- ✅ Custom tags and conditions
- ✅ AI uses simplified GAS abilities

---

## 🧪 Challenges & Solutions

- GAS pipeline was complex at first, so I rebuilt everything in C++ to understand it fully.
- Animation timing was tricky — solved with notifies and montage tasks.

---

## 🔬 Technical Highlights

- Extended `UAbilitySystemComponent` with helper methods.
- Used `AttributeSet` classes for health, stamina, and damage logic.
- Bound input actions to abilities via Enhanced Input and GAS tags.
- Created a custom tag system to manage ability states and rules.

---

## 🧠 Lessons Learned

- GAS is powerful but needs structure. C++ helped me understand it better.
- Tags are key for flexible ability design.
- Syncing gameplay and animation is critical for good combat feel.
- Layered animations improved movement and combat blending.
- Well-organized montages make combo management easier.

---

## 📦 Tech Stack

`Unreal Engine 5.5 • C++ • GAS • Animation Montage • Gameplay Tags • Enhanced Input`

---
