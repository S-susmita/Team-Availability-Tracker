# Team Availability Tracker

A real-time dashboard for tracking team member availability with database synchronization.

## Features

- 📊 **Real-time Statistics** - View total members, available/unavailable counts, and availability rate
- 🔄 **Instant Updates** - Toggle availability with immediate visual feedback
- 💾 **Database Persistence** - All changes are stored in SQLite database
- 🎨 **Beautiful UI** - Modern, responsive design with smooth animations
- ⚡ **Optimistic Updates** - Instant UI updates with automatic rollback on errors
- 📱 **Responsive** - Works seamlessly on desktop, tablet, and mobile devices

## Tech Stack

### Frontend
- **React** - UI library
- **Vite** - Build tool and dev server
- **CSS3** - Styling with modern features

### Backend
- **Express** - Web framework
- **SQLite** (better-sqlite3) - Database
- **CORS** - Cross-origin resource sharing

## Getting Started

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn

### Installation

1. Install dependencies:
```bash
npm install
```

2. Start the backend server:
```bash
npm run server
```

3. In a new terminal, start the frontend dev server:
```bash
npm run dev
```

4. Open your browser to `http://localhost:3000`

## Project Structure

```
team-availability-tracker/
├── server/
│   ├── index.js           # Express API server
│   └── availability.db    # SQLite database (auto-created)
├── src/
│   ├── components/
│   │   ├── UserCard.jsx       # Individual user card component
│   │   ├── UserCard.css
│   │   ├── StatsPanel.jsx     # Statistics panel component
│   │   └── StatsPanel.css
│   ├── App.jsx            # Main app component
│   ├── App.css
│   ├── main.jsx           # React entry point
│   └── index.css          # Global styles
├── index.html
├── vite.config.js
├── package.json
└── README.md
```

## API Endpoints

### GET `/api/users`
Get all users with their availability status.

**Response:**
```json
[
  {
    "id": 1,
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "role": "Frontend Developer",
    "available": 1,
    "last_updated": "2024-01-15 10:30:00"
  }
]
```

### PATCH `/api/users/:id/availability`
Update a user's availability status.

**Request Body:**
```json
{
  "available": true
}
```

**Response:**
```json
{
  "id": 1,
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "role": "Frontend Developer",
  "available": 1,
  "last_updated": "2024-01-15 10:35:00"
}
```

### GET `/api/stats`
Get availability statistics.

**Response:**
```json
{
  "total": 8,
  "available": 6,
  "unavailable": 2
}
```

## Key Implementation Details

### State Synchronization
- **Optimistic Updates**: UI updates immediately when toggling availability
- **Server Sync**: Changes are sent to the backend API
- **Error Handling**: Automatic rollback if the server update fails
- **Stats Refresh**: Statistics panel updates after each change

### Conditional Rendering
- User cards change border color based on availability (green/red)
- Status badges display "Available" or "Unavailable" with different colors
- Toggle switches reflect the current state visually

### Database Schema
```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE,
  role TEXT NOT NULL,
  available BOOLEAN NOT NULL DEFAULT 1,
  last_updated DATETIME DEFAULT CURRENT_TIMESTAMP
)
```

## Customization

### Adding New Users
You can add users directly to the database or modify the seed data in `server/index.js`:

```javascript
const seedData = [
  ['Your Name', 'email@example.com', 'Your Role', 1],
  // Add more users...
];
```

### Styling
All component styles are in their respective `.css` files. The app uses CSS custom properties for easy theme customization.

## Future Enhancements

- [ ] Add user authentication
- [ ] Implement user roles and permissions
- [ ] Add availability scheduling
- [ ] Export availability reports
- [ ] Add real-time WebSocket updates
- [ ] Integrate with calendar systems
- [ ] Add notification system

## License

MIT
