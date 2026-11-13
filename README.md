# NOVA AI – Offline Android Assistant

Kotlin + Jetpack Compose app that runs GGUF language models (Qwen, Llama, Gemma…) fully on-device through llama.cpp.
Chats, memories and PDFs stay on the phone. Internet is only used if you tap **Download** for a model.

## Get the APK (pick ONE way)

### A) No installation on your PC – build in the cloud (easiest)
1. Create a free GitHub account and a new empty repository.
2. Upload everything in this folder (keep the `.github` folder) to the repository.
3. Open the **Actions** tab → **Build APK** → **Run workflow**. Wait ~10–15 minutes.
4. Open the finished run → **Artifacts** → download `NovaAI-debug-apk` → unzip → `app-debug.apk`.

### B) Android Studio
1. Install Android Studio (Koala or newer). Open this folder as a project.
2. Let Gradle sync (needs internet the first time: it downloads Gradle, the NDK 26.1, CMake 3.22.1 and llama.cpp tag b5200 automatically).
3. Build → Build APK(s). Output: `app/build/outputs/apk/debug/app-debug.apk`.

## Install on the phone
1. Copy `app-debug.apk` to the phone, open it, and allow "Install unknown apps" for your file manager/browser.
2. Requirements: Android 8.0+, 64-bit (arm64) phone, 4 GB RAM or more recommended.
3. Open NOVA AI → menu → **AI models** → download a model (Qwen2.5 1.5B is a good start) or import your own `.gguf`.
4. After the model is installed, everything works in airplane mode.

## User guide
- **Chat**: type and press send; replies stream live. ■ stops generation. "+" starts a new chat. Side menu = history (🗑 deletes one chat).
- **Memory**: say "Remember that…", "My name is…", "I prefer…". Manage under Settings → Saved memories.
- **Voice**: 🎤 listens once and sends your words. Settings → "Read replies aloud" enables text-to-speech. For offline speech recognition, install the offline language pack in Android settings (Google app → Offline speech recognition).
- **PDF**: 📎 picks a PDF. Ask questions about it, or tap **Summarize**. Works with text PDFs (not scanned images).
- **Study mode**: top-right subject menu (Mathematics, Physics, Chemistry, Biology, Computer Science, English) makes NOVA explain step by step with examples.
- **Settings**: theme, context size, threads, reply length, temperature, delete all history.
- **Low memory**: the app checks free RAM before loading a model and tells you to pick a smaller one or lower the context size.

## Model suggestions (Q4_K_M)
| Phone RAM | Model |
|---|---|
| 3–4 GB | Qwen2.5 0.5B, Llama 3.2 1B |
| 6 GB | Qwen2.5 1.5B, Gemma 2 2B |
| 8 GB+ | Qwen2.5 3B, Llama 3.2 3B (import manually) |

## Project layout
- `app/src/main/cpp` – CMake + JNI wrapper around llama.cpp (fetched at build time)
- `app/src/main/java/com/nova/ai` – `MainActivity` (UI), `ChatViewModel` (logic), `data/` (Room DB, settings), `util/` (PDF, voice), `llm/` (JNI bridge)

## Notes
- The APK is a debug-signed build, fine for personal use.
- Pure-CPU inference: expect roughly 3–15 tokens/sec depending on phone and model.
