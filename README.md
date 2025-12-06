# Ozu Frontend - Admin Portal

A modern React + TypeScript admin portal for real-time rider tracking connected to your FastAPI backend.

## ✨ Features

- 🗺️ **Live Interactive Map** - OpenStreetMap with Leaflet
- 🎯 **Real-Time Rider Tracking** - Color-coded markers (🟢 Available, 🟡 Assigned, 🔴 In Transit)
- ⚡ **WebSocket Integration** - Instant updates via Socket.IO
- 🔄 **Auto Polling** - Fallback polling every 5 seconds
- 📊 **Modern UI** - Tailwind CSS + shadcn/ui components
- 🚀 **Fast Development** - Vite with HMR

## 🛠️ Tech Stack

- **React 18** with TypeScript
- **Vite** for fast development and builds
- **Tailwind CSS** for styling
- **shadcn/ui** for UI components
- **Leaflet + React-Leaflet** for maps
- **Socket.IO Client** for real-time updates
- **Fetch API** for HTTP requests

## 📦 Quick Start

```bash
# 1. Install dependencies
cd frontend
npm install

# 2. Create .env file
echo "VITE_BACKEND_BASE_URL=http://localhost:8000" > .env

# 3. Start development server
npm run dev

# 4. Open http://localhost:3000
```

## 🔧 Backend Requirements

Your FastAPI backend needs:

### HTTP Endpoint
```
GET /riders/live
Returns: Array of rider objects with { id, name, status, lat, lng, zone, phone, activeShipmentId, updatedAt }
```

### WebSocket
```
Socket.IO path: /ws/riders
Event: 'rider_update' with rider object
```

### Rider Status Types
- `available` - Rider is free (🟢 Green)
- `assigned` - Job allocated, not moving (🟡 Yellow)
- `in_transit` - On the way (🔴 Red)
- `offline` - Not active (⚫ Gray)

See **[SETUP.md](./SETUP.md)** for detailed setup instructions and backend configuration.

## 📂 Project Structure

```
frontend/
├── public/                      # Static assets
├── src/
│   ├── components/
│   │   ├── ui/                 # shadcn/ui components (Button, Card, Badge)
│   │   └── map/                # Map components (RiderMarker, MapLegend, MapToolbar)
│   ├── pages/
│   │   └── AdminPortal/        # Admin portal pages (RiderMap, index)
│   ├── hooks/                  # Custom hooks (useRiders)
│   ├── lib/                    # Utilities (api, socket, utils)
│   ├── types/                  # TypeScript types (rider, shipment)
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── .env                        # Environment variables
├── package.json
├── SETUP.md                    # Detailed setup guide
└── vite.config.ts
```

## 🎨 UI Components

Pre-configured shadcn/ui components:
- ✅ Button
- ✅ Card (with Header, Title, Content)
- ✅ Badge

## 🗺️ Map Features

- **Auto-fit bounds** to show all riders
- **Popup on click** with rider details
- **Color-coded markers** by status
- **Live legend** at bottom-left
- **Refresh button** at top-left
- **Last update timestamp** in header

## 🔄 Real-Time Updates

The app uses **dual update strategy**:
1. **WebSocket (Socket.IO)** - Instant updates when available
2. **Polling** - Fetches data every 5s as fallback

## 🚀 Available Scripts

```bash
npm run dev      # Start development server (port 3000)
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

## 🐛 Troubleshooting

See **[SETUP.md](./SETUP.md)** for common issues and solutions.

## 🔐 CORS Configuration

Make sure your FastAPI backend allows CORS from `http://localhost:3000`:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

## 📈 Future Enhancements

The right panel is a placeholder. You can add:
- Live order feed
- Rider performance analytics
- Shipment timeline
- Customer management
- Real-time notifications

Tell me what you need and I'll wire it up!

## 📝 License

Private - Ozu Project
