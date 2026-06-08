<<<<<<< HEAD
## Setup

1. Clone the `main` branch, 

```bash
$> git clone --depth=1 https://github.com/shivay_couchbase/kotlin-cblite-vector-search-rag
cd cblite-kotlin-vector-search
```

2. [Get an API key from Google AI Studio](https://ai.google.dev/gemini-api/docs/api-key) to use the Gemini API. Copy 
the key and paste it in `local.properties` present in the root directory of the project,

```
geminiKey="AIza[API_KEY_HERE]"
```

Perform a Gradle sync, and run the application. 



=======
# CBLite Vector Search RAG - Run As-Is Setup

## WHAT'S NEEDED

### System Requirements
- macOS 11+ / Windows 10+ / Linux
- 16GB RAM minimum
- 50GB disk space
- Internet connection

### Install Order

#### 1. Java JDK 17
```bash
# macOS
brew install openjdk@17

# Windows - Download from:
https://www.oracle.com/java/technologies/downloads/#java17

# Linux (Ubuntu)
sudo apt-get install openjdk-17-jdk
```

**Verify:**
```bash
java -version
```

---

#### 2. Android Studio
```
Download from: https://developer.android.com/studio
Install and run through setup wizard
```

**In Android Studio Setup:**
- Install Android SDK 34
- Install Android SDK Build-Tools 34.x.x
- Install Android Emulator
- Accept all licenses

**Verify location:**
```bash
# macOS/Linux
echo $ANDROID_HOME
# Should be: $HOME/Library/Android/sdk (macOS)
#            $HOME/Android/Sdk (Linux)

# Windows
echo %ANDROID_HOME%
# Should be: C:\Users\[YourName]\AppData\Local\Android\sdk
```

---

#### 3. Create Virtual Device
```bash
# In Android Studio:
Tools → Device Manager → Create Device
- Select: Pixel 7
- API Level: 34
- Name: Pixel_7_API_34
- RAM: 4GB minimum

# OR command line:
emulator -list-avds
emulator @Pixel_7_API_34
```

---

#### 4. Get Google Gemini API Key
```
Visit: https://ai.google.dev/gemini-api/docs/api-key
Click: "Get API Key"
Copy: Your key (starts with AIza...)
```

---

#### 5. Clone Project
```bash
cd ~/projects  # or your preferred location

git clone https://github.com/shivay_couchbase/kotlin-cblite-vector-search-rag

cd kotlin-cblite-vector-search-rag/cblite-kotlin-vector-search
```

---

#### 6. Set API Key
```bash
# In project root directory (cblite-kotlin-vector-search):

echo 'geminiKey="AIzaSyD_YOUR_ACTUAL_KEY_HERE"' > local.properties
```

**Verify:**
```bash
cat local.properties
# Should show: geminiKey="AIzaSyD_..."
```

---

## RUN THE PROJECT

### Step 1: Start Emulator
```bash
# Terminal 1
emulator @Pixel_7_API_34
# Wait for Android home screen (takes 30-60 seconds)
```

### Step 2: Build & Run
```bash
# Terminal 2 - In project root
cd cblite-kotlin-vector-search

# Make gradlew executable
chmod +x gradlew

# Clean build
./gradlew clean

# Build project
./gradlew build

# Run app
./gradlew run

# OR one command:
./gradlew clean build && ./gradlew run
```

### Step 3: App Launches
- App installs on emulator
- Chat screen appears
- Ready to use

---

## TEST THE APP

1. **Open app** (should show Chat screen)
2. **Upload document:**
   - Tap folder icon (top right)
   - Tap PDF or DOCX button
   - Select document from device storage
   - Wait for processing (30 seconds)
3. **Ask question:**
   - Go back to chat
   - Type question in input field
   - Tap send
   - Wait 5-20 seconds
   - Answer appears

---

## QUICK COMMAND REFERENCE

```bash
# Setup (one time)
brew install openjdk@17                    # Install Java
# Download Android Studio from web link
./gradlew clean build                      # Build project
echo 'geminiKey="..."' > local.properties  # Add API key

# Running (every time)
emulator @Pixel_7_API_34                   # Start emulator
./gradlew run                              # Run app

# Debugging
adb logcat                                 # View logs
./gradlew clean                            # Clean build
./gradlew build --refresh-dependencies     # Force refresh

# Other useful commands
emulator -list-avds                        # List emulators
adb devices                                # List connected devices
./gradlew installDebug                     # Install only
./gradlew uninstall                        # Remove app
```

---

## ENVIRONMENT SETUP (Optional but Recommended)

```bash
# Add to ~/.zshrc or ~/.bash_profile

export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/tools

# Reload:
source ~/.zshrc
```

---

## DEPENDENCIES (Auto-Downloaded by Gradle)

```
CouchDB Lite 3.1          - Local database
Jetpack Compose 1.5       - UI framework
Hilt 2.46                 - Dependency injection
Kotlin Coroutines 1.7     - Threading
Google Generative AI 0.6  - Gemini API
ONNX Runtime (Android)    - Embeddings
Apache POI                - Document reading
```

All downloaded automatically via `./gradlew build`

---

## FILE STRUCTURE

```
cblite-kotlin-vector-search/
├── app/
│   ├── src/main/
│   │   ├── java/com/ml/shivay_couchbase/docqa/
│   │   │   ├── MainActivity.kt
│   │   │   ├── domain/
│   │   │   │   ├── QAUseCase.kt
│   │   │   │   ├── embeddings/SentenceEmbeddingProvider.kt
│   │   │   │   └── llm/GeminiRemoteAPI.kt
│   │   │   ├── data/
│   │   │   │   ├── DatabaseManager.kt
│   │   │   │   └── ChunksDB.kt
│   │   │   └── ui/screens/
│   │   │       ├── ChatScreen.kt
│   │   │       └── DocsScreen.kt
│   │   └── assets/
│   │       ├── all-MiniLM-L6-V2.onnx
│   │       └── tokenizer.json
│   └── build.gradle.kts
├── gradle/
├── local.properties    ← ADD YOUR API KEY HERE
├── build.gradle.kts
└── settings.gradle.kts
```

---

## TROUBLESHOOTING

| Problem | Solution |
|---------|----------|
| `gradle: command not found` | `chmod +x gradlew` |
| `ANDROID_HOME not set` | Create local.properties with `sdk.dir=/path/to/sdk` |
| `API key invalid` | Regenerate from ai.google.dev, verify starts with `AIza` |
| `Emulator won't start` | Increase RAM in Device Manager or use `-wipe-data` |
| `Build fails` | Run `./gradlew clean` then `./gradlew build` |
| `App crashes immediately` | Check logcat: `adb logcat \| grep -i exception` |
| `No answer from Gemini` | Check internet, verify API key, check Gemini API quota |

---

## THAT'S IT

**Total setup time: 30-45 minutes**

```bash
# One-time setup (copy-paste):
brew install openjdk@17
# Download Android Studio from browser
cd ~/projects
git clone https://github.com/shivay_couchbase/kotlin-cblite-vector-search-rag
cd kotlin-cblite-vector-search-rag/cblite-kotlin-vector-search
echo 'geminiKey="AIzaSyD_YOUR_KEY"' > local.properties
chmod +x gradlew
./gradlew clean build

# Every time you want to run:
emulator @Pixel_7_API_34  # Terminal 1
./gradlew run             # Terminal 2
```

Done! 🚀
>>>>>>> 799f6690086fdee3a2ade800e8d1702606296a92
