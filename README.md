# WORK.LOG // BRUTALIST TASK TRACKER

```
██╗    ██╗ ██████╗ ██████╗ ██╗  ██╗   ██╗      ██████╗  ██████╗ 
██║    ██║██╔═══██╗██╔══██╗██║  ██║  ███║     ██╔═══██╗██╔════╝ 
██║ █╗ ██║██║   ██║██████╔╝███████║  ╚██║     ██║   ██║██║  ███╗
██║███╗██║██║   ██║██╔══██╗╚════██║   ██║     ██║   ██║██║   ██║
╚███╔███╔╝╚██████╔╝██║  ██║     ██║   ██║  ██╗╚██████╔╝╚██████╔╝
 ╚══╝╚══╝  ╚═════╝ ╚═╝  ╚═╝     ╚═╝   ╚═╝  ╚═╝ ╚═════╝  ╚═════╝ 
                                                      v1.1.0-prod
```

An uncompromising, high-contrast, high-impact **Neo-Brutalist Work Logging System** and **Real-Time Task Tracker**. Designed for heavy-duty logs, fast status tracking, and 100% private database configuration.

🌍 **Live Demo:** [https://JabadeSusheelKrishna.github.io/work-tracker/](https://JabadeSusheelKrishna.github.io/work-tracker/)

---

## ⚡ CORE SPECIFICATIONS

* **Vibrant Neo-Brutalist Interface:** High-contrast borders, pixel-hard drop shadows, typography powered by **JetBrains Mono**, and micro-animations that make logging work feel premium and responsive.
* **Real-Time Synchronization:** Backed by **Firebase Cloud Firestore** with real-time listeners (`onSnapshot`). Changes on one tab or device sync immediately across all connected instances.
* **100% Zero-Leak Security Portal (`⚙️ DB Setup`):** Protects your keys from GitHub Pages public history. Paste your Firebase configurations directly within your browser, where it remains saved securely in local `localStorage` without ever touching a Git commit!
* **Worker Logs & Communications:** Add rich inline comments, timestamped worker notes, and live external reference links (Figma, GitHub, Notion docs) to any task dynamically.
* **Dynamic Search & Sorting Console:** Instantly filter tasks by title keyphrase, state category (`To Do`, `In Progress`, `Done`), sorted sequence, and auto-generated tag clouds.

---

## 🛠️ INSTALLATION & ARCHITECTURE

The entire application compiles into a single, highly-optimized static frontend payload, requiring no heavy framework compile steps.

```
index.html             # Core DOM structure, Brutalist design system, and ES6 Firebase Engine.
README.md              # System Manual & Technical Overview.
deployment_guide.md    # Security blueprints and GitHub deployment procedures.
```

### Local Dev Launch:
Since the app utilizes modern **ES6 JavaScript Modules (ESM)** to interact with Firebase, the browser's CORS policy requires running the app via a local server.

```bash
# Using Python
python3 -m http.server 8000

# Or using Node.js
npx http-server -p 8000
```
Open your browser and navigate to `http://localhost:8000` to start logging.

---

## 🔌 FIREBASE CONNECTIVITY INITIALIZATION

To connect the application to your database safely:

1. Create a web application in the [Firebase Console](https://console.firebase.google.com/).
2. Enable **Cloud Firestore** inside your project console.
3. Open your deployed **WORK.LOG** page.
4. Navigate to the **⚙️ DB Setup** tab in the header.
5. Paste your Firebase web app configuration block:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```
6. Click **Connect & Initialize Database** to connect in real-time.

---

## 🔒 RECOMMENDATIONS: FIRESTORE SECURITY RULES

Since database connectivity is established purely client-side, secure your database from unauthorized writes. Go to your **Firebase Console > Firestore Database > Rules** and deploy the following schema-validated ruleset:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tasks/{taskId} {
      // Validate schema and field lengths for optimal security
      allow read, write: if request.resource.data.title is string
                          && request.resource.data.title.size() > 0
                          && request.resource.data.title.size() < 100
                          && request.resource.data.emoji is string
                          && request.resource.data.emoji.size() <= 4
                          && request.resource.data.progress in ['todo', 'in-progress', 'done']
                          && request.resource.data.createdAt is number;
      
      allow delete: if true;
    }
  }
}
```

---

## 🚀 LICENSE & PROTOCOLS

Developed under the **MIT License**. Keep editing, keep building, keep logs clean.
Designed for heavy-duty storage. Built to inspire bold designs.
