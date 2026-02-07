# Realtime Device Tracker

A real-time device tracking application built with Node.js, Express, Socket.IO, and Leaflet maps.

## Features

- Real-time location tracking
- Interactive map visualization using Leaflet
- WebSocket communication with Socket.IO

## Tech Stack

- **Backend:** Node.js, Express.js
- **Real-time Communication:** Socket.IO
- **Frontend:** EJS, Leaflet.js
- **Styling:** CSS

## Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd realtime-device-tracker
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the server:
   ```bash
   node app.js
   ```

4. Open your browser and navigate to:
   ```
   http://localhost:3000
   ```

## Project Structure

```
├── app.js              # Main server file
├── package.json        # Project dependencies
├── public/
│   ├── css/
│   │   └── style.css   # Stylesheets
│   └── js/
│       └── script.js   # Client-side JavaScript
└── views/
    └── index.ejs       # Main view template
```

## License

MIT
