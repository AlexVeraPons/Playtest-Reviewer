## Playtesting Reviewer — README

*A no code Unity toolkit for capturing gameplay video + gameplay metrics and reviewing them side by side.*

---

### 1. What is it?

Playtesting Reviewer adds a **non-intrusive recording pipeline** to your Unity project:

* **Recorder prefab** – captures gameplay video to `StreamingAssets`.
* **Metric Recorder component** – hooks any C# event or property so you can log deaths, hits, scores, etc.
* **Review player** – replays the video and overlays every metric track on an interactive timeline, either inside the Unity Editor or in a tiny standalone viewer.&#x20;

---

### 2. Quick Start

1. **Import the package**
   Double-click the supplied `.unitypackage`. A folder called `LatestReview` appears under `Assets/`.&#x20;
2. **Add FFmpeg**
   Drop the `FFmpeg` folder into **`Assets/StreamingAssets/`** (create the folder if it doesn’t exist).&#x20;
3. **Place the recorder**
   Drag **`Recorder.prefab`** into the first scene that should start recording. That’s all video + metric capture now happens automatically on Play mode or in a build.&#x20;
4.**Start adding metrics**
   You can now attach the metric recorder monobehavior and start tracking events.&#x20;
   
---

### 3. Metric Recorder

1. Open the GameObject that raises the event (e.g., the `Player` script).
2. **Add Component → Metric Recorder**.
3. Configure:

   * **Metric Name** – e.g., `Deaths`.
   * **Color** – any color for the timeline track.
   * **Events To Track** – drag the component that exposes the event, then pick the event (`OnDeath`, `OnHit`, etc.).
   * *(Optional)* **Properties To Track** – drag the same component again and tick any public property (`CurrentLife`, `MaxLife`, …).&#x20;

---

### 4. Reviewing Inside the Editor

1. End Play mode ⇒ a new folder `ReviewOutput/YYYY-MM-DD-HH-mm-ss/` appears.
2. Double click the generated **Review Sciptable Object** asset, then hit **Play** in the Review window.
3. Click **“＋”** to and select the metric you want to add; scrub with the mouse wheel, **Ctrl + wheel** to zoom in and out;
4. Click anywhere in the timel.&#x20;

---

### 5. Reviewing Outside the Editor

Two options after you build the game:

| Option                         | Steps                                                                                                                                                                                         | When to use                                                            |   
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- | 
| **Import back into Unity**     | `Tools → Playtesting → Import Review` → select the JSON file, then the video. A new `.review` asset is generated and can be opened as usual.                                                  | You still have the project on your machine.                            |   
| **Standalone Reviewer (.exe)** | Grab the minimal Reviewer build from the GitHub repo. Drop the whole `ReviewOutput` sub-folder into `%APPDATA%/PlaytestingReviews/`, press **Refresh**, choose your review, and hit **Play**. | You just need a quick look or a playtester sent you files. |   


---

### Q&A 
| Issue | Fix |
|-------|-----|
| *No video recorded* | Ensure **`ffmpeg`** is executable and placed in `StreamingAssets`. |
| *Metric not appearing* | Confirm you attached **Metric Recorder** to an event that is being called, also make sure the recorder prefab is added. |
| *Where can I find the reviews after playing?* | This depends, if you played in Unity the output is located at Assets -> PlaytestReviewer -> ReviewOutput. If you are playing in a standalone version you can find the review in the Output folder in the build folder.|
