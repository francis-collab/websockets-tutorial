# Connect Four Multiplayer — WebSockets Tutorial 🎮     

---
                                                                                                                        ## Introduction

This project is a real-time, browser-based implementation of **Connect Four**, built using **JavaScript (frontend)** and **Python with the `websockets` library (backend)**. It walks through progressive deployment from local testing to global multiplayer access using **GitHub Pages** and **Koyeb*

---

## Features

- **Real-time multiplayer** with WebSockets
- **Spectator mode** via watch-only links
- Stateless frontend with no database
- Works on modern desktop and mobile browsers
- Free-to-deploy using GitHub + Koyeb

---

## Project Directory Structure

```
websockets-tutorial/
├── connect4.py          # Game logic
├── app.py               # WebSocket server (Python)
├── main.js              # Frontend WebSocket connector
├── connect4.js          # Game renderer and handler
├── connect4.css         # Styling for the game board
├── index.html           # Main HTML page
├── requirements.txt     # Declares 'websockets' dependency
├── Procfile             # Instructs Koyeb how to start the server
└── README.md            # Project documentation
```

---

## Local Development

### 1. Serve the frontend

```bash
python3 -m http.server 8000
```

### 2. Run the WebSocket server

```bash
python3 app.py
```

Then open your browser and visit:

```
http://localhost:8000
```

---

## Deployment

### Backend on Koyeb

Ensure the following updates are made:

- `app.py` uses `os.environ.get("PORT")`
- Health check route `/healthz` responds with `200 OK`
- `Procfile` contains:

```
web: python app.py
```

- `requirements.txt` contains:

```
websockets
```

**Steps to deploy:**

1. Push the project to GitHub
2. Go to [https://www.koyeb.com](https://www.koyeb.com)
3. Connect your GitHub account
4. Select the repository
5. Set:
   - Branch: `main`
   - Root directory: `/`
6. Set health check:
   - Protocol: HTTP
   - Path: `/healthz`
7. Deploy and wait for the WebSocket backend to go live

---

### Frontend on GitHub Pages

1. Push all frontend files (`index.html`, `main.js`, etc.) to the root of the repository
2. In `main.js`, define the WebSocket server as follows:

```js
function getWebSocketServer() {
  if (window.location.host === "francis-collab.github.io") {
    return "wss://websockets-tutorial-francis-collab.koyeb.app/";
  } else if (window.location.host === "localhost:8000") {
    return "ws://localhost:8001/";
  } else {
    throw new Error("Unsupported host: " + window.location.host);
  }
}
```

3. Use it like this:

```js
const websocket = new WebSocket(getWebSocketServer());
```

4. On GitHub:
   - Go to **Settings → Pages**
   - Source: `main` branch
   - Folder: `/ (root)`
   - Click **Save**

Your app will be available at:

```
https://francis-collab.github.io/websockets-tutorial/
```

---

## How to Play

- Visit the page in your browser
- Click “Join” to receive a game link
- Share that link with a friend, or open in a second tab
- Take turns — and may the smartest strategist win!

---

## License

This project is licensed under the MIT License.
See the `LICENSE` file for more details.

---

## Author

This application was designed and developed by **Francis Mutabazi**.
You can find more of my work on [GitHub](https://github.com/francis-collab).

---

## Acknowledgment

Built by following the official `websockets` Python tutorial.
