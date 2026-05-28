# SwapTxT Changelog (v1.0.7)

## 🆕 New Features (ฟีเจอร์ใหม่)

### 1. Smart Background Auto-Updater
- **Silent Periodic Checks**: Automatically checks for updates in the background around 7:00 AM and between 5:00 PM - 8:00 PM (17:00-20:00).
- **Non-Intrusive UI**: Replaced the disruptive popup with a clean, orange "Update Available" button in the Settings window.

### 2. Multi-Language Q&A / Reply Localization
- **Dynamic System Prompt**: The AI Q&A prompt now automatically adapts to the user's selected Native Language.
- **Language-Neutral Parsing**: Replaced hardcoded Thai markers with language-neutral logic, ensuring perfect output parsing regardless of the user's language settings.
- **Clipboard Context**: Clicking a reply option now copies the exact translated reply correctly.

### 3. Graceful Single-Instance Enforcement
- **Mutex Lock & IPC**: Added Inter-Process Communication to prevent multiple instances of SwapTxT from running simultaneously.
- **Beautiful Alert UI**: If a user accidentally opens the program again, a sleek custom window alerts them and automatically brings the existing instance's Settings window to the foreground.

---

## 🎨 UI & UX Improvements (การปรับปรุงดีไซน์)

### 1. Streamlined Scrollbar
- **Slim ScrollViewer**: Updated the Q&A result pane's scrollbar to use the modern, thin `DarkScrollViewer` style, matching the rest of the app's aesthetic.

### 2. Context-Aware Command Menu
- **Dynamic Feature Hiding**: When using Google Translate, AI-specific features (Q&A, Summarize, Grammar) are automatically hidden from the Floating Menu, leaving only the "Translate" option to reduce clutter.
