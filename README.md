# 🧠 Custom Visual Studio Code with Built-In Wingman AI

This project is a fully customized fork of [Visual Studio Code (OSS)](https://github.com/microsoft/vscode) where the [Wingman AI](https://github.com/RussellCanfield/wingman-ai) extension has been deeply integrated as a **native, built-in component**. The extension runs on startup, is hidden from the Extensions UI, and provides intelligent code suggestions and automation without being removable or visible to the user.

The build process is managed via a **GitHub Actions CI/CD pipeline**, making it fully reproducible and cloud-executed — even on machines that can't compile VS Code locally due to hardware limitations.

---

## 🚀 Project Goals

- 📦 Package Wingman AI into VS Code as a **built-in** extension
- 🚫 Prevent user from disabling/uninstalling it
- ☁️ Offload heavy build tasks to GitHub Actions
- 🧪 Ensure the build is **reproducible** and **extensible**
- ✅ Produce a final `.exe` or `.zip` version of VS Code with AI integrated

---

## 🔧 Tech Stack

| Category           | Tools & Technologies                         |
|-------------------|-----------------------------------------------|
| Editor Base        | [VS Code OSS](https://github.com/microsoft/vscode) |
| AI Integration     | [Wingman AI](https://github.com/RussellCanfield/wingman-ai) |
| Build Tools        | Gulp, Node.js, NPM                           |
| DevOps & CI/CD     | GitHub Actions                               |
| System Integration | Electron, Windows `.exe` packaging (user-setup) |
| Configuration      | `extensions.json`, `product.json`, `gulpfile.js` |

---

## 🛠️ Setup & How It Works

### 1. Fork & Clone
```bash
git clone https://github.com/<your-username>/vscode.git
cd vscode
```

### 2. Add Wingman AI
Clone the extension into VS Code's internal folder:
```bash
git clone https://github.com/RussellCanfield/wingman-ai.git
xcopy wingman-ai extensions\wingman-ai /E /I /Y
```

Ensure subfolders like `shared/` and `views-ui/` exist inside `wingman-ai`.

### 3. Register as Built-In
Create or update:
📄 `build/extensions.json`
```json
[
  { "name": "wingman-ai", "repo": "local" }
]
```

### 4. Setup GitHub Actions Workflow
Create `.github/workflows/build.yml` with:
- Node install
- Extension dependency install
- Gulp build
- Upload artifact step

See: [build.yml](.github/workflows/build.yml)

### 5. Trigger CI Build
```bash
git add .
git commit -m "Add Wingman AI as built-in + CI setup"
git push origin main
```

Go to GitHub → **Actions tab** → Wait for the run → Download artifact from “vscode-portable”.

---

## ✅ What’s Working

- Wingman AI loads at startup with **no UI listing**
- All build steps (install, compile, bundle) succeed on GitHub Actions
- Project is fully reproducible with clear workflow
- Integrated seamlessly into the official VS Code architecture

---

## ⚠️ Known Issues

- The `.exe` portable build occasionally fails on GitHub CI due to VS Code packaging limitations
- Local builds are resource-intensive and may freeze low-spec systems
- File-based dependencies like `shared/` and `views-ui/` must be manually preserved

---

## 📂 Folder Structure Summary

```
vscode/
├── .github/
│   └── workflows/
│       └── build.yml
├── extensions/
│   └── wingman-ai/
│       ├── shared/
│       ├── views-ui/
│       └── package.json
├── build/
│   └── extensions.json
├── product.json
├── .vscode/
└── gulpfile.js
```

---

## 📤 CI/CD Pipeline Highlights

- Runs on `push` to `main`
- Uses `windows-latest` runner
- Builds `vscode-win32-x64-user-setup`
- Uploads `.exe`/`.zip` from `build/user-setup/`
- Separate `npm install` for root and wingman extension

---

## 📈 What I Learned

- Deep understanding of VS Code’s internal architecture
- Native packaging and extension hiding techniques
- GitHub Actions, caching, dependency resolution
- Real-world debugging of `node-gyp`, `npm`, `gulp`, and Electron

---

## ✍️ Author

**Ayush Chhanchar**  
🔗 [LinkedIn](https://linkedin.com/in/ayushchhanchar)  
📁 [GitHub Portfolio](https://github.com/ayushchhanchar)  
📧 [Email me](mailto:your.email@example.com)

---

## ⭐ Final Notes

This repo reflects my practical experience with real-world developer tooling. I built it to demonstrate my ability to work with:
- Large open-source codebases
- Low-level extension integration
- Cloud automation pipelines
- DevOps and system-level customization

Feel free to fork this repo or reach out if you'd like to collaborate!
