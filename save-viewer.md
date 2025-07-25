# 💾 Save Viewer – View, Search, and Manage Your JSON Save Files

> A Unity Editor tool to instantly inspect and manage your game's save files in one elegant interface.

---

## 🎯 What Is It?

Save Viewer is a custom Unity Editor window designed to help developers view, inspect, and manage all JSON-based save files directly within the editor.

Whether you're debugging save states, inspecting corrupted data, or testing new features — this tool puts everything at your fingertips.

---

## ✨ Features

- 📂 Automatically detects and lists all save `.json` files in your persistent save folder
- 🔍 Search bar for quickly filtering specific files
- 👁️ View content of each save file in a scrollable popup
- 🗑️ Delete individual save files
- 🧹 Clear **all** save files with one click
- 📏 Displays file size and last modified timestamp

---

## 🖼️ Preview

![Save Viewer](media/dev-hub/save-system-1.png)
![Save Viewer](media/dev-hub/save-system-2.png)

---

## 💡 Use Cases

- Quickly verify gameplay save states
- Reset corrupted or test save data
- Review analytics or player progress in development
- Works perfectly during testing and prototyping phases

---

---

## 🛠️ How It Works

- Uses `Application.persistentDataPath` to locate save files
- Filters `.json` files and reads metadata (size, date)
- Provides per-file and global operations (view/delete)
> Editor-only utility – not included in final game build.

---

## ⚙️ Requirements

- Unity 2021+
- JSON-based save system (optional formatting layer for reading)

---

## 📦 Tech Stack

`Unity • C# • EditorWindow • File I/O • JSON • GUI Utility`

---

## 🧠 Why I Built It

During development, constantly digging into save folders manually was slowing down my workflow. This tool gives a centralized, readable panel to search, inspect, and control all data during debugging sessions — no explorer, no console, no hassle.

---
