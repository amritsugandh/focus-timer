<div align="center">

# 🌱 Focus Timer

### *Stay Focused. Grow Your Plant. Master Your Time.*

A minimalist Pomodoro timer that holds you accountable through intelligent tab detection and a virtual plant companion that lives or dies based on your focus.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Made with Love](https://img.shields.io/badge/Made%20with-❤️-red.svg)](https://github.com/amritsugandh)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[Live Demo](#) • [Documentation](./docs) • [Report Bug](https://github.com/amritsugandh/focus-timer/issues) • [Request Feature](https://github.com/amritsugandh/focus-timer/issues)

</div>

---

## 🎯 What is Focus Timer?

Focus Timer is not just another Pomodoro app. It's your **accountability partner** that uses the browser's Visibility API to detect when you lose focus. Switch tabs during a work session? Your timer resets and your virtual plant suffers. Stay focused for the full 25 minutes? Watch your plant bloom! 🌻

### The Problem It Solves

Traditional timers let you cheat. You can switch tabs, browse social media, and still claim you "worked" for 25 minutes. Focus Timer eliminates this by:

- 🔍 **Detecting tab switches** in real-time
- ⏱️ **Resetting your timer** when you lose focus
- 🌿 **Visualizing consequences** through your plant's health
- 💪 **Building real focus habits** through accountability

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| ⏲️ **Pomodoro Timer** | Classic 25-minute work blocks with countdown display |
| 👁️ **Tab Detection** | Uses Document Visibility API to track your focus |
| 🚨 **Consequence System** | Timer resets + plant degrades when you break focus |
| 🌱 **Virtual Plant** | Visual companion that reflects your focus quality |
| 🎨 **Minimal UI** | Distraction-free design to keep you in the zone |
| 📱 **No Dependencies** | Pure HTML, CSS, and JavaScript - works anywhere |
| 🔒 **Privacy First** | Everything runs locally in your browser |

---

## 🚀 Quick Start

### Option 1: Direct Use (Fastest)

1. **Download** or clone this repository
2. **Open** `index.html` in any modern browser
3. **Click Start** and begin your focus session!

```bash
# Clone the repository
git clone https://github.com/amritsugandh/focus-timer.git

# Navigate to the folder
cd focus-timer

# Open in browser (Windows)
start index.html
```

### Option 2: Run Locally

No build process needed! Just open the HTML file:

```bash
# Windows
start index.html

# macOS
open index.html

# Linux
xdg-open index.html
```

---

## 🎮 How to Use

### Starting Your First Session

1. **Open the app** in your browser
2. **Click "Start"** to begin a 25-minute focus session
3. **Stay on the tab** - your plant starts healthy 🌱
4. **Complete 25 minutes** - your plant blooms! 🌻

### What Happens When You Lose Focus?

- ⚠️ Switch tabs → Timer resets to 25:00
- 🥀 Your plant degrades or dies
- 🔄 You must start over

### Tips for Success

- 📵 Close distracting tabs before starting
- 🎧 Use headphones to minimize interruptions
- ☕ Keep water/coffee nearby to avoid leaving
- 📝 Plan your task before hitting start

---

## 🏗️ Project Architecture

```
focus-timer/
├── 📄 index.html          # Main HTML structure
├── 🎨 styles.css          # Minimal styling
├── 🚀 app.js              # Application entry point
├── ⏱️ timer.js            # Timer countdown logic
├── 👁️ visibility.js       # Tab detection module
├── 🌱 plant.js            # Plant visualization
├── 🧠 state.js            # State management
├── 🖼️ ui.js               # UI controller
├── 📚 docs/
│   ├── requirements.md    # Detailed requirements
│   └── design.md          # Architecture & design
├── 📝 README.md
├── 📜 LICENSE
└── 🚫 .gitignore
```

### Component Overview

```
┌─────────────────────────────────────────┐
│        User Interface Layer             │
│   (HTML/CSS - Timer Display & Plant)    │
└─────────────────────────────────────────┘
                    ↕
┌─────────────────────────────────────────┐
│      Application State Manager          │
│  (Central state & event coordination)   │
└─────────────────────────────────────────┘
                    ↕
┌──────────────┬──────────────┬───────────┐
│ Timer Module │ Visibility   │  Plant    │
│              │ Detector     │  Renderer │
└──────────────┴──────────────┴───────────┘
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **HTML5** | Semantic structure |
| **CSS3** | Minimal, clean styling |
| **Vanilla JavaScript** | No frameworks - pure JS |
| **Document Visibility API** | Tab detection |
| **LocalStorage** | Session persistence (future) |

### Browser Compatibility

- ✅ Chrome 33+
- ✅ Firefox 18+
- ✅ Safari 7+
- ✅ Edge 12+
- ✅ Opera 20+

---

## 🧪 Testing

The project uses a dual testing approach:

- **Unit Tests** - Specific examples and edge cases
- **Property-Based Tests** - Universal correctness properties using [fast-check](https://github.com/dubzzz/fast-check)

### Test Coverage

- ✅ 100% state transition coverage
- ✅ 100% consequence system logic
- ✅ 100% visibility detection
- ✅ 90%+ UI controller functions
- ✅ 10 correctness properties validated

---

## 📋 Roadmap

### Version 1.0 (Current)
- [x] Basic Pomodoro timer
- [x] Tab detection
- [x] Plant visualization
- [x] Consequence system

### Version 1.1 (Planned)
- [ ] Sound notifications
- [ ] Break timer (5 minutes)
- [ ] Session counter
- [ ] Keyboard shortcuts

### Version 2.0 (Future)
- [ ] Session history & statistics
- [ ] Multiple plant types to unlock
- [ ] Dark mode support
- [ ] Progressive Web App (PWA)
- [ ] Customizable work/break durations
- [ ] Export session data

---

## 🤝 Contributing

Contributions make the open-source community amazing! Any contributions you make are **greatly appreciated**.

### How to Contribute

1. **Fork** the project
2. **Create** your feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Contribution Ideas

- 🐛 Report bugs
- 💡 Suggest new features
- 📝 Improve documentation
- 🎨 Enhance UI/UX
- ✅ Add tests
- 🌍 Add translations

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

This means you can:
- ✅ Use commercially
- ✅ Modify
- ✅ Distribute
- ✅ Private use

---

## 👤 Author

**Amrit Sugandh**

- 🐙 GitHub: [@amritsugandh](https://github.com/amritsugandh)
- 💼 LinkedIn: [Connect with me](https://linkedin.com/in/amritsugandh)
- 📧 Email: [Contact](mailto:amritsugandh@example.com)

---

## 🙏 Acknowledgments

- 🍅 Inspired by the [Pomodoro Technique](https://francescocirillo.com/pages/pomodoro-technique) by Francesco Cirillo
- 🌱 Plant emoji designs from Unicode Standard
- 🎨 Design inspiration from minimalist productivity tools
- 💻 Built with passion for focus and productivity

---

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/amritsugandh/focus-timer?style=social)
![GitHub forks](https://img.shields.io/github/forks/amritsugandh/focus-timer?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/amritsugandh/focus-timer?style=social)

---

<div align="center">

### ⭐ Star this repo if it helps you stay focused!

**Made with ❤️ and ☕ by Amrit Sugandh**

[⬆ Back to Top](#-focus-timer)

</div>
A minimalist web-based Pomodoro timer that keeps you accountable through tab detection and a virtual plant companion.

## 🎯 Overview

Focus Timer helps you maintain focus during 25-minute work sessions by detecting when you switch tabs. Break your focus, and your virtual plant suffers the consequences. Stay focused, and watch it thrive!

## ✨ Features

- **25-Minute Pomodoro Timer** - Classic Pomodoro technique implementation
- **Tab Detection** - Uses Document Visibility API to detect when you leave the tab
- **Consequence System** - Timer resets and your plant degrades when you break focus
- **Virtual Plant Companion** - Visual feedback that reflects your focus quality
- **Distraction-Free UI** - Minimal design to keep you in the zone

## 🚀 Demo

[Live Demo](#) _(Coming soon)_

## 🛠️ Tech Stack

- **HTML5** - Semantic structure
- **CSS3** - Minimal, clean styling
- **Vanilla JavaScript** - No frameworks, pure JS
- **Document Visibility API** - Tab detection

## 📦 Installation

1. Clone the repository:
```bash
git clone https://github.com/amritsugandh/focus-timer.git
cd focus-timer
```

2. Open `index.html` in your browser:
```bash
# On Windows
start index.html

# On Mac
open index.html

# On Linux
xdg-open index.html
```

That's it! No build process, no dependencies.

## 🎮 How to Use

1. Click the **Start** button to begin a 25-minute focus session
2. Stay on the Focus Timer tab to keep your plant healthy
3. If you switch tabs, the timer resets and your plant degrades
4. Complete the full 25 minutes to see your plant bloom!

## 🏗️ Project Structure

```
focus-timer/
├── index.html     
