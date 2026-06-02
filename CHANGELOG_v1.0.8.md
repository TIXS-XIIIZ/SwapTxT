# SwapTxT Changelog (v1.0.8)

## 🆕 New Features (ฟีเจอร์ใหม่)

### 1. Default AI Model
- **gemini-3.1-flash-lite**: Changed default AI model to `google/gemini-3.1-flash-lite`.

### 2. Setup UI Polish
- **Native Rounded Corners**: Redesigned the setup screen to match the main app's dark theme aesthetics perfectly. Implemented native Windows 11 DWM smooth rounded corners for the setup UI with seamless fallback to Region-clipping on Windows 10.
- **Visual Artifacts Fixed**: Prevented color bleeding and pixelated jaggy edges around the setup window border.

### 3. Self-Contained Installer (ติดตั้งง่าย ไม่ต้องลง .NET)
- **Zero-Dependency Installer**: The new `SwapTxT_Install_v1.0.8.exe` bundles the .NET 8.0 runtime directly — users can install and run SwapTxT with a single click, no pre-requisites required.
- **Compact Size**: Despite bundling the runtime, aggressive LZMA2 compression keeps the installer around 15-20 MB.
- **Full Installer Experience**: Sets up a Start Menu shortcut, optional Desktop icon, and registers an Uninstaller — just like a professional Windows application.

---

## 🐛 Bug Fixes (แก้บั๊ก)

### 1. Floating Icon — Intermittent Ctrl+C / Ctrl+V Failure
- **Root Cause**: When the Floating Icon feature was enabled, the heuristic text-selection routine cleared the clipboard before sending a synthetic `Ctrl+C`. If the user manually pressed `Ctrl+V` during that window, the clipboard was empty and nothing was pasted.
- **Fix — Sequence-Number Guard**: Replaced `ClearClipboardSafe()` with `GetClipboardSequenceNumber()`. The clipboard is now only restored if it was actually modified by the heuristic — preserving any content the user had copied beforehand.
- **Fix — Real-Time Key Detection**: Added `GetAsyncKeyState()` polling during the heuristic wait period. If `Ctrl`, `C`, or `V` is detected as physically held down, the heuristic aborts immediately and yields control back to the user's intended keypress.

### 2. Grammar Check — Highlighted Text Not Processed
- **Root Cause**: The AI was occasionally confused about which part of the combined message was the "text to analyze" vs. the instruction itself.
- **Fix**: Added an explicit `--- TEXT TO ANALYZE ---` delimiter at the end of the system prompt, giving the AI a clear, unambiguous boundary between instructions and input content.

---

## 📝 Documentation (เอกสาร)

### HOW_TO_UPDATE_VERSION.md
- Documented the new **Launcher-based build architecture** (`SwapTxT.exe` + `SwapTxT_Core.exe`).
- Added a unified `build_release.ps1` script to automate publishing, compiling the launcher, and packaging the zip.

### 2. Auto-Update Setup Screen (UX Improvement)
- **Launcher Redesign**: Replaced the basic PowerShell message boxes with a branded, custom Windows Forms UI.
- **Visual Feedback**: When checking for or installing .NET 8.0, users now see a clean "Setting Up" screen with a marquee progress bar instead of an unresponsive pause, preventing the perception of a launch failure.
- Output installer is now named `SwapTxT.zip` / `SwapTxT_Install_v1.0.8.exe` for clarity.
- Added `installer.iss` Inno Setup script to the project for repeatable, one-click installer creation.
