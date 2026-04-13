# Realtime Device Tracker

Realtime Device Tracker is a small Node.js application that shares a browser's current geographic position over Socket.IO and renders it on an interactive Leaflet map. When one client sends location updates, every connected client receives them in real time and sees the marker move on the map.

## What It Does

- Tracks device location in the browser using the Geolocation API.
- Broadcasts latitude and longitude updates to connected clients with Socket.IO.
- Displays each connected device as a live marker on a Leaflet map.
- Removes a marker automatically when a client disconnects.

## Tech Stack

- **Backend:** Node.js, Express.js
- **Real-time transport:** Socket.IO
- **View layer:** EJS
- **Maps:** Leaflet + OpenStreetMap tiles
- **Styling:** Custom CSS

## Requirements

- Node.js 18 or newer is recommended.
- A modern browser with Geolocation support.
- Location permission enabled in the browser.

## Installation

1. Install dependencies:

   ```bash
   npm install
   ```

2. Start the application:

   ```bash
   npm start
   ```

3. Open the app in your browser:

   ```
   http://localhost:3000
   ```

## How It Works

The app uses a very small server/client flow:

1. The Express server serves the EJS page and static assets from the public folder.
2. The browser loads Socket.IO and Leaflet from CDN links.
3. The client script requests geolocation access from the browser.
4. On every location update, the client emits a send-location event to the server.
5. The server broadcasts the update to all connected clients as receive-location.
6. Each client updates or creates a marker for that socket ID.
7. When a socket disconnects, its marker is removed from the map.

## Project Structure

```text
.
├── app.js
├── package.json
├── README.md
├── public/
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── script.js
└── views/
    └── index.ejs
```

## File Overview

### app.js

Creates the Express server, attaches Socket.IO, serves static files, and defines the root route that renders the main view.

### views/index.ejs

Contains the HTML shell for the app, including the map container and the CDN links for Leaflet and Socket.IO.

### public/js/script.js

Handles browser geolocation, sends live position updates, initializes the map, and manages markers for connected users.

### public/css/style.css

Contains the visual styling for the application layout and map container.

## Socket Events

### send-location

Emitted by the client whenever the browser provides a new location update.

Payload example:

```json
{
  "latitude": 28.6139,
  "longitude": 77.2090
}
```

### receive-location

Broadcast by the server to all clients when any connected device sends a new location.

Payload example:

```json
{
  "id": "socket-id",
  "latitude": 28.6139,
  "longitude": 77.2090
}
```

### user-disconnected

Broadcast by the server when a socket disconnects so clients can remove the corresponding marker.

## Development Notes

- The app currently uses the browser's current position only; it does not persist history or track routes over time.
- Each connected socket is treated as a separate device marker.
- The map centers itself on the latest reported location.
- The app uses public CDN assets for Leaflet and Socket.IO, so an internet connection is required unless those dependencies are bundled locally.

## Browser and Location Caveats

- Most browsers require geolocation to run in a secure context. Localhost is usually allowed during development.
- If the browser blocks location access, the app will still load, but no live marker will appear.
- Accuracy depends on the device, browser, and network conditions.

## Scripts

- `npm start` starts the server with Node.js.
- `npm test` is currently a placeholder and does not run a test suite.

## Customization Ideas

- Add authentication so only approved users can connect.
- Store location history in a database.
- Draw paths or breadcrumbs instead of only showing the latest marker.
- Add user labels, status indicators, or device metadata.
- Replace the CDN assets with local dependencies for offline packaging.

## Troubleshooting

### Map does not load

- Confirm the server is running and the browser can reach http://localhost:3000.
- Check the browser console for missing CDN resources or JavaScript errors.

### Location is not updating

- Make sure location permissions are enabled for the site.
- Verify that the browser and device support the Geolocation API.
- Try a different browser if permission prompts do not appear.

### Marker does not move

- Open the browser console and confirm Socket.IO is connected.
- Check whether the browser is returning position updates at all.

## License

MIT
