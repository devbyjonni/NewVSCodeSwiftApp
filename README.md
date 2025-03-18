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
import Foundation

let projectName = "MyNewSwiftProject"
let homeDir = FileManager.default.homeDirectoryForCurrentUser
let projectPath = homeDir.appendingPathComponent("Developer").appendingPathComponent(projectName)

// Step 1: Create project directory
do {
    let developerPath = homeDir.appendingPathComponent("Developer")

    if !FileManager.default.fileExists(atPath: developerPath.path) {
        try FileManager.default.createDirectory(
            at: developerPath, withIntermediateDirectories: true, attributes: nil)
    }

    try FileManager.default.createDirectory(
        at: projectPath, withIntermediateDirectories: true, attributes: nil)
    print("✅ Created project directory: \(projectPath.path)")
} catch {
    print("❌ Error creating project directory: \(error)")
    exit(1)
}

// Step 2: Initialize Swift package
let process = Process()
process.launchPath = "/usr/bin/env"
process.arguments = ["swift", "package", "init", "--type", "executable"]
process.currentDirectoryPath = projectPath.path

do {
    try process.run()
    process.waitUntilExit()
    print("✅ Initialized Swift package")
} catch {
    print("❌ Error initializing Swift package: \(error)")
    exit(1)
}

// Step 3: Locate `main.swift`
let sourcesPath = projectPath.appendingPathComponent("Sources")
let nestedSourcesPath = sourcesPath.appendingPathComponent(projectName)
let mainSwiftFile: URL

if FileManager.default.fileExists(atPath: nestedSourcesPath.path) {
    // If `Sources/<ProjectName>/` exists, use that
    mainSwiftFile = nestedSourcesPath.appendingPathComponent("main.swift")
} else {
    // Otherwise, use `Sources/main.swift`
    mainSwiftFile = sourcesPath.appendingPathComponent("main.swift")
}

// Step 4: Overwrite `main.swift` with custom content
let mainSwiftContent = """
    import Foundation

    class App {
        func run() {
            print("New Swift App Running! 🚀")
        }
    }

    let app = App()
    app.run()
    """

do {
    try mainSwiftContent.write(to: mainSwiftFile, atomically: true, encoding: .utf8)
    print("✅ Updated \(mainSwiftFile.path)")
} catch {
    print("❌ Error updating main.swift: \(error)")
    exit(1)
}

// Step 5: Create VS Code settings for Swift development
let vscodeFolder = projectPath.appendingPathComponent(".vscode")
let settingsFile = vscodeFolder.appendingPathComponent("settings.json")

let vscodeSettings: [String: Any] = [
    "swift.path": "/usr/bin/swift",
    "swift.lldb.suppressMissingModuleWarning": true,
    "swift.lldb.displayFormat": "auto",
]

do {
    try FileManager.default.createDirectory(
        at: vscodeFolder, withIntermediateDirectories: true, attributes: nil)
    let jsonData = try JSONSerialization.data(
        withJSONObject: vscodeSettings, options: .prettyPrinted)
    try jsonData.write(to: settingsFile)
    print("✅ Created VS Code settings file")
} catch {
    print("❌ Error creating VS Code settings: \(error)")
    exit(1)
}

print("\n🚀 Swift project setup completed successfully! 🎉")
print("👉 Navigate to the project: cd \(projectPath.path)")
print("👉 Open in VS Code: code \(projectPath.path)")
print("👉 Build the project: swift build")
print("👉 Run the project: swift run")

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
