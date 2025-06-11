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

> *Preview of melee combat using Gameplay Ability System and animation-based hit detection.*

---

## 💻 What I Did

- Implemented **all core gameplay systems** using Unreal’s Gameplay Ability System (GAS), including light/heavy attacks, dashing, stamina drain, blocking, and damage-over-time effects.
- Wrote all **ability logic, attribute sets, effect calculations, and activation conditions** in C++ for full performance control and flexibility.
- Created a **custom `UAbilitySystemComponent`** wrapper with helper functions for applying instant, duration-based, and periodic effects.
- Developed a **combo chain system** using **animation montage section transitions** and `AbilityTask_PlayMontageAndWaitForEvent`, allowing conditional continuation into different attack types (light → heavy → finisher).
- Integrated **Ability Tags and Tag Queries** to control:
  - Input gating (e.g., cannot dash while stunned)
  - Blocking interrupts
  - Cooldowns and cost validation
- Built a **robust gameplay effect system** that handles:
  - Buffs and debuffs with durations
  - Stamina cost per ability
  - Health regeneration and status ailments (burn, poison, bleed)

- Architected and synced **HUD/UI elements** for attributes like Health, Stamina, and Cooldowns — updated in real-time using GAS replication and delegates.

### 🔄 Animation System Integration

- Set up **upper-body animation layering** using **Blend Poses by bool** and **Slot Nodes**, allowing attacks to play on the upper body while retaining locomotion in the lower body.
- Created and managed **animation layers** for armed state, blocking stance.
- Used `AnimNotifies` to trigger damage windows, particle effects, camera shakes, and sound cues — precisely synced to montage timings.
- Configured **animation blueprint state machines** to reflect GAS states (e.g., stunned, knockdown) and transition smoothly with blend times.



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
  `Ability.Melee.Attack.Basic`,   `Ability.Melee.Attack.Strong`,  `State.Stunned`,  `Cooldown.Dash`
  and used Tag Queries in effect application and AI logic.
  
---

## 🧠 Lessons Learned

- Gained deep understanding of **GAS architecture**, including attribute replication, execution policies, cost/cooldown mechanics, and client prediction.
- Understood how **animation syncing** can make or break the feel of combat, and how GAS can enhance this by cleanly separating logic and animation timing.
- Learned to design reusable **Ability Blueprints** while keeping the logic in C++ for performance and clarity.
- Built a mental model of how **Tags, Effects, and Abilities** interact to drive modular combat design.
- Improved my ability to debug GAS by using **visual tools and breakpoints** in ability flow.

---

## 📦 Tech Stack

`Unreal Engine 5.5 • C++ • Gameplay Ability System • Animation Montage • Gameplay Tags • Enhanced Input • GAS Debugging Tools`

---
