# 📝 Notion Desktop (Electron Wrapper)

A lightweight Electron-based desktop wrapper for **Notion.so**, built for Ubuntu to avoid heavy browser usage and provide a native-like app experience.

---

## 🚀 NPM & System Requirements

### Install System Dependencies
```bash
sudo apt update
sudo apt install rpm
sudo apt-get install dpkg-dev fakeroot
```

---

## 📦 Install Node Modules
```bash
npm install electron
npm install --save-dev @electron-forge/cli
```

---

## 🧩 Update `main.js`
```javascript
const { app, BrowserWindow } = require('electron');

function createWindow() {
  const win = new BrowserWindow({
    width: 1200,
    height: 800,
    webPreferences: {
      nodeIntegration: false,
      contextIsolation: true,
    },
  });

  win.loadURL('https://www.notion.so');
  win.webContents.openDevTools(); // Optional
}

app.whenReady().then(() => {
  createWindow();
  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) createWindow();
  });
});

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit();
});
```

---

## 🛠 Update `package.json`
```jsonc
{
  "main": "main.js",
  "description": "A desktop app for Notion.so, built with Electron",
  "scripts": {
    "start": "electron .",
    "make": "electron-forge make"
  },
  "forge": {
    "make_targets": {
      "linux": ["deb", "rpm"]
    }
  }
}
```

---

## ▶️ Run Electron App
```bash
npm start
```

---

## 🏗 Build App (DEB/RPM)
```bash
npx electron-forge import
npm run make
```

Output packages will be generated inside:

```
out/make/
```

---

## 📥 Install App on Ubuntu
```bash
sudo dpkg -i out/make/deb/x64/notion-app_1.0.0_amd64.deb
```

---

## ❌ Uninstall App
```bash
dpkg -l | grep notion
sudo dpkg -r notion-app
```