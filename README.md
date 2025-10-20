# RETranslate - Real-Time Audio Translation for macOS

RETranslate is a macOS application that provides real-time audio translation using system audio capture (via BlackHole) and free translation services. Perfect for translating YouTube videos, Netflix content, and online meetings in real-time.

## 🚀 Key Features

- **System Audio Capture**: Capture audio from YouTube, Netflix, Zoom using BlackHole virtual audio device
- **Real-time Translation**: Instant speech-to-text and translation with floating overlay
- **Free Translation**: Uses MyMemory API - no API keys required
- **Multi-language Support**: Supports 50+ language pairs
- **Floating Overlay**: Subtitle-style overlay on top of videos
- **Translation History**: Review and mark important translations

## 📦 Installation

### Option 1: Download DMG (Recommended)
1. Go to [Releases](https://github.com/[your-username]/RETranslate/releases)
2. Download the latest `RETranslate.dmg`
3. Open the DMG and drag RETranslate to Applications folder
4. Follow the BlackHole setup guide below

### Option 2: Build from Source
1. Clone this repository
2. Open `RETranslate.xcodeproj` in Xcode
3. Build and run (requires macOS 12.0+ and Xcode 14+)

### BlackHole Setup (Required for System Audio)
To capture system audio from YouTube, Netflix, etc., you need BlackHole virtual audio driver:

1. Download [BlackHole](https://github.com/ExistentialAudio/BlackHole/releases) (BlackHole.2ch.pkg)
2. Install the package and restart your Mac
3. Open **Audio MIDI Setup** app
4. Create a **Multi-Output Device**
5. Select both **Built-in Output** and **BlackHole 2ch**
6. Set system audio output to the **Multi-Output Device**

📋 **Detailed setup guide**: See `BLACKHOLE_SETUP.md` for step-by-step instructions with screenshots.

### No API Keys Required! 🎉
RETranslate now uses free translation services:
- **Speech Recognition**: Google Cloud Speech (built-in API key)
- **Translation**: MyMemory API (free, no registration needed)

## 🎯 Quick Start

1. **Install BlackHole** (see setup guide above)
2. **Launch RETranslate**
3. **Set audio source** to "System Audio (BlackHole)" in Settings
4. **Open a YouTube video** in your browser
5. **Click "Start Video Translation"** in RETranslate
6. **Enjoy real-time subtitles!** 🎉

### Floating Overlay
Enable **Settings > Appearance > Floating Overlay** to show translations on top of videos like subtitles.

## 🛠️ Development & Building

### Creating DMG for Distribution

1. **Build the app**:
```bash
xcodebuild -project RETranslate.xcodeproj -scheme RETranslate -configuration Release BUILD_DIR=$PWD/build
```

2. **Create DMG**:
```bash
chmod +x scripts/create_dmg.sh
scripts/create_dmg.sh
```

3. **GitHub Releases**: Push a tag (e.g., `v1.0.0`) to trigger the GitHub Actions workflow that builds and uploads the DMG automatically.

See `PUBLISHING.md` for code signing and notarization details.

### Required Permissions

The app requires these macOS permissions:
- **Microphone**: For audio capture
- **Screen Recording**: For floating overlay (macOS 10.15+)

## 🔧 Troubleshooting

### No Audio Captured
- Ensure BlackHole is installed and Multi-Output Device is configured
- Check system audio output is set to Multi-Output Device
- Grant Microphone permission when prompted

### No Translation Appearing
- Check internet connection
- Ensure video has audio (silent videos won't translate)
- MyMemory API may have hit daily limit (~1000 characters)

### Overlay Not Visible
- Grant Screen Recording permission in System Preferences > Security & Privacy
- Check overlay opacity settings

## Geliştirici Notları

### Proje Yapısı
```
RETranslate/
├── AudioCapture.swift          # Ses yakalama modülü
├── ScreenCapture.swift         # Ekran yakalama (macOS 12.3+)
├── SpeechToTextService.swift   # STT API entegrasyonları
├── TranslationService.swift    # Çeviri API entegrasyonları
├── RETranslateManager.swift    # Ana koordinasyon sınıfı
├── ContentView.swift           # Ana UI
├── SettingsView.swift          # Ayarlar sayfası
├── FloatingOverlayWindow.swift # Overlay penceresi
└── RETranslate.entitlements    # macOS izinleri
```

### API Entegrasyonları

#### OpenAI Whisper
```swift
// Multipart form-data ile WAV dosyası gönderimi
POST https://api.openai.com/v1/audio/transcriptions
```

## 🔒 Privacy & Security

- Audio data is processed in real-time and not stored
- No personal data collection
- All network traffic uses HTTPS encryption
- Translation services: MyMemory (free) + Google Cloud STT (built-in key)

## 🎬 Supported Platforms

- ✅ **YouTube** (all videos)
- ✅ **Netflix** (in browser)  
- ✅ **Prime Video**, **Disney+**, **Hulu**
- ✅ **Zoom**, **Microsoft Teams** meetings
- ✅ **Any app** with audio (VLC, QuickTime, etc.)

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## ⭐ Support

If you find RETranslate useful, please give it a star on GitHub!

---

**Made with ❤️ by RE Technology**# RETranslate
