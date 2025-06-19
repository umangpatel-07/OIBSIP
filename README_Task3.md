
# 📱 Flightscry – Android UI Prototype

A proof-of-concept Android app built with **Backpack**, showcasing a simple, elegant flight itinerary UI.

---

## ✅ Requirements
- Android Studio (Recommended version: **Electric Eel** or later)
- Kotlin
- SDK: API 33 – Android Tiramisu

---

## 🚀 Getting Started

### 1. Install Android Studio
Follow [this official guide](https://developer.android.com/codelabs/basic-android-kotlin-compose-install-android-studio#0)

> ⚠️ Avoid Android Studio Dolphin due to rendering bugs with Backpack.

---

### 2. Create a New Project
- Template: **Empty Activity**
- Language: **Kotlin**
- Minimum SDK: **API 33**
- Project Name: `Flightscry`

---

### 3. Run Your App
- Click the ▶️ run button to launch the emulator.
- Use built-in emulator if no physical device is available.
- If emulator issues arise, refer to [troubleshooting guide](https://developer.android.com/studio/run/emulator-troubleshooting).

---

## 📦 Add Backpack Dependency

Open `build.gradle (Module)` and add the following to `dependencies`:

```gradle
implementation 'net.skyscanner.backpack:backpack-android:43.0.0'
```

Then click **"Sync Now"** when prompted.

---

## 🛠️ Build the UI

### What to Include in `activity_main.xml`:

#### 1. Flight Info Card
- Flight number: e.g., `Flight: AB123`

#### 2. Departure Card
- Airport code: e.g., `LHR`
- Departure time: e.g., `08:45`

#### 3. Arrival Card
- Airport code: e.g., `JFK`
- Arrival time: e.g., `13:30`

### UI Components to Use:
- `BpkCardView` for grouping sections
- `BpkText` for headings and labels
  - Use: `style="@style/bpkTextHeading1"`
- `LinearLayout` (vertical) for stacking items
- Set card attribute `cornerStyle="large"` for aesthetics

You can edit this from the **Code** or **Design** tab in Android Studio.

---

## 🧪 Test the App
- Press ▶️ Run
- Check the virtual device
- Confirm layout and dummy data are displayed as expected

---

## 📤 Submit Your Work

### Step 1: Push to GitHub

```bash
git init
git add .
git commit -m "Flightscry UI built with Backpack"
git remote add origin https://github.com/YOUR_USERNAME/flightscry-task3
git push -u origin main
```

### Step 2: Submit the Repo URL

```
https://github.com/YOUR_USERNAME/flightscry-task3
```

---

## 📚 Helpful Resources
- [Layout Editor](https://developer.android.com/studio/write/layout-editor)
- [Android Themes](https://developer.android.com/develop/ui/views/theming/themes)
- [Backpack Components](https://www.skyscanner.design/latest/welcome-to-backpack-Mtf5OEo4)
- [Declaring Layout](https://developer.android.com/develop/ui/views/layout/declaring-layout)
