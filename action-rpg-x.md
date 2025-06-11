# ⚔️ Action RPG X – GAS

> A fast-paced, third-person action RPG inspired by *God of War*, developed entirely in C++ using Unreal Engine’s Gameplay Ability System (GAS).

---

## 🗂 Overview

- **Genre**: Action RPG / Melee Combat  
- **Platform**: PC (Unreal Engine 5)  
- **Engine**: Unreal Engine 5.5 
- **Primary Language**: C++ (99%)  
- **Core System**: Gameplay Ability System (GAS)  

---

## 📸 Media

<p align="center">
  <a href="https://www.youtube.com/watch?v=zm9DI4lpowE" target="_blank">
    <img src="https://i3.ytimg.com/vi/zm9DI4lpowE/maxresdefault.jpg" width="600" alt="Watch the Gameplay Trailer">
  </a>
</p>

> *Preview of melee combat using Gameplay Ability System and animation-based hit detection.*

---

## 💻 What I Did

- Implemented **all gameplay mechanics** using GAS, including combat, stamina, dashing, and status effects.
- Created a **custom ability system component and actor attribute sets** in C++ for full control and performance.
- Integrated **combo chains and animation montages** using GAS abilities with section-based transitions.
- Designed a **scalable effect system** for buffs, DOTs, and resource drains using GameplayEffectModifiers.
- Built an ability queuing system and **ability tags** for input gating and conditional triggers.
- Created debugging tools to visualize active abilities, cooldowns, and applied effects in real-time.
- Designed the **HUD and UI logic** to reflect dynamic GAS-driven attributes like HP, Stamina, and Ability Cooldowns.

---

## 🔧 Key Features

- ✅ Fully C++-based GAS implementation with modular design  
- ✅ Dynamic melee combo system using animation notifies and GAS section triggers  
- ✅ Attribute Set: Health, Stamina, Damage, Knockback Resistance  
- ✅ Custom Gameplay Tags and Tag Queries for ability logic  
- ✅ Ability cooldowns, resource cost, conditional activation  
- ✅ AI uses simplified version of GAS for status effects and attacks  
- ✅ Extensible effect system with GameplayEffect calculations  

---

## 🧪 Challenges & Solutions

> **Challenge**: Understanding the full pipeline of GAS from input → ability execution → effect application.  
> **Solution**: I built a complete end-to-end flow in C++, replacing most of the default Blueprint setups to fully internalize the flow and increase performance flexibility.

> **Challenge**: Animation sync with ability logic (e.g., damage only applies during swing).  
> **Solution**: Used `AnimNotifies` and `AbilityTask_PlayMontageAndWaitForEvent` to tightly couple animations with timed events.

---

## 🔬 Technical Deep Dive

- **Custom Ability System Component**  
  Extended `UAbilitySystemComponent` with helper methods for queuing, checking tag states, and applying manual effects.

- **C++ Attribute Sets**  
  Used derived `UAttributeSet` classes to define and replicate HP, Stamina, Attack Power, and more. Used GameplayEffectModifiers with additive/multiply scalars.

- **Input Binding**  
  Used `Enhanced Input System` to bind input actions to GameplayAbilities through `Ability Input IDs`, activated via tags.

- **Tag System**  
  Designed a custom tag schema like:
  Ability.Melee.Attack.Basic
  Ability.Melee.Attack.Strong
  State.Stunned
  Cooldown.Dash
  and used Tag Queries in effect application and AI logic.
  
---

## 🧠 Lessons Learned

- Gained deep understanding of **GAS architecture**, including attribute replication, execution policies, cost/cooldown mechanics, and client prediction.
- Understood how **animation syncing** can make or break the feel of combat, and how GAS can enhance this by cleanly separating logic and animation timing.
- Learned to design reusable **Ability Blueprints** while keeping the logic in C++ for performance and clarity.
- Built a mental model of how **Tags, Effects, and Abilities** interact to drive modular combat design.
- Improved my ability to debug GAS by creating **visual tools and breakpoints** in ability flow.

---

## 📦 Tech Stack

`Unreal Engine 5.5 • C++ • Gameplay Ability System • Animation Montage • Gameplay Tags • Enhanced Input • GAS Debugging Tools`

---
