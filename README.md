

# QiYi Smart Cube Web

This is a browser-based interface for connecting and interacting with a [QiYi Smart Cube](https://speedcubeshop.com/products/qiyi-ai-3x3-bluetooth-smart-cube-speed-version) using JavaScript, HTML, and CSS. It communicates with the cube via Bluetooth Low Energy (BLE) and visualises the cube’s state in real time.

This project is inspired by [Flying-Toast/qiyi_smartcube_protocol](https://github.com/Flying-Toast/qiyi_smartcube_protocol), which reverse-engineered the QiYi protocol and built a similar tool in Rust. This version reimplements key ideas using only web technologies for easier accessibility and demonstration.

---

## 🔧 Features

- 📡 Connect to a QiYi Smart Cube via Web Bluetooth API  
- 🧩 Live display of all 6 faces of the cube using emojis  
- 🔄 Track moves and update cube state in real time  
- 🔋 Display battery level  
- 🧼 Reset cube to solved state  
- 🔐 Encrypt/decrypt messages using AES-128 ECB (thanks to [aes-js](https://github.com/ricmoo/aes-js))

---

## ⚙️ How It Works

1. Upon connecting, the app sends an `App Hello` message using the cube’s MAC address (reversed).
2. The cube responds with a `Cube Hello` message containing the initial state and battery info.
3. All communication is encrypted using AES-128 ECB with a fixed key.
4. Cube states are parsed and displayed visually on the webpage using emojis.
5. Move and state changes trigger updates and (sometimes) acknowledgements.
6. A "Reset to Solved State" button sends a `Sync State` message to resynchronise the cube.

---

## 📋 Prerequisites

- A QiYi Bluetooth Smart Cube  
- A modern browser with [Web Bluetooth API](https://web.dev/bluetooth/) support (e.g. Chrome)  
- Permissions to use Bluetooth from the browser  

---

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/qiyi-smartcube-web.git
   cd qiyi-smartcube-web
   ```

2. Open `index.html` in a compatible browser (you may need to serve it via a local web server for Bluetooth to work reliably).

3. Click **“Connect Cube”**, enter the cube’s MAC address (e.g. `CC:A3:00:00:25:13`), and watch the cube’s state appear!

---

## 📁 Project Structure

- `index.html` – Single-page app with embedded styles and scripts  
- No external backend – All logic is handled client-side  

---

## 🧠 Acknowledgements

- Protocol details based on the excellent reverse engineering work by [Flying-Toast/qiyi_smartcube_protocol](https://github.com/Flying-Toast/qiyi_smartcube_protocol)
- AES encryption via [aes-js](https://github.com/ricmoo/aes-js)


---

## 💡 Tip: Remembering Your MAC Address

By default, the app prompts you to enter your cube's MAC address every time you connect.  
To make development and use easier, you can hardcode a default value into the prompt by modifying this line in `index.html`:

```js
const macStr = prompt("Enter cube MAC address (e.g. CC:A3:00:00:25:13)\nIf you are using Google Chrome, you can find it at:\nchrome://bluetooth-internals/#devices");
```

Change it to:

```js
const macStr = prompt("Enter cube MAC address (e.g. CC:A3:00:00:25:13)\nIf you are using Google Chrome, you can find it at:\nchrome://bluetooth-internals/#devices", "<YOUR MAC ADDRESS>");
```

This way, the MAC address will auto-fill in the prompt every time you connect.


---

## 📜 License

MIT – feel free to use, modify, and build upon this project.
