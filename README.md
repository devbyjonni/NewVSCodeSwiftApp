# NewVSCodeSwiftApp

Follow these steps to create a new **Swift** project from scratch using **Visual Studio Code** on **Mac**.

---

## Check if Swift is installed:

```bash
swift --version
```

If Swift is not installed, download the latest version from [Swift.org](https://swift.org).

### Install Swift Extensions in VS Code

Install the following extensions from the VS Code Marketplace:

- [Swift for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=sswg.swift-lang)
- [CodeLLDB (for debugging)](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb)

---

## 🚀 Quick Setup Script

```bash
cd ~/Developer
mkdir MyNewSwiftProject
cd MyNewSwiftProject
swift package init --type executable
echo 'import Foundation

class App {
    func run() {
        print("New Swift App Running! 🚀")
    }
}

let app = App()
app.run()' > Sources/main.swift
```

###  Download .gitignore for Swift

Download the recommended `.gitignore` file for Swift projects:

(This file is hosted in GitHub’s official `.gitignore` repository: `GitHub/gitignore`.)

```bash
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Swift.gitignore 
```

### Verify Configuration

```bash
swift build
swift run
```

---


### Open and Run the Project in VS Code

```bash
code .
swift build
swift run
```

### Initialize & Commit to Git

```bash
git init
git add .
git commit -m "Initial commit with Swift .gitignore"
git log
git status
```


---

✅ **All Set!**
