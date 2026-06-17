# Bangalore Borewell Sensor Dashboard

A frontend web dashboard for visualizing Bengaluru borewell sensor locations, BBMP ward boundaries, water-level trends, and discharge data on top of OpenStreetMap.

This repository contains only the **frontend** files for the dashboard. The downloader, database, and API are handled separately by the backend service.

---

## Live Dashboard

After GitHub Pages is enabled, the dashboard will be available at:

```text
https://VishwasPrabhakara.github.io/bbmp-borewell-dashboard/
```

---

## What This Frontend Does

The dashboard:

- Loads BBMP ward boundaries from the bundled `bbmpwards.zip` file.
- Displays borewell sensors on an OpenStreetMap basemap.
- Fetches sensor and water-level data from the deployed backend API.
- Shows ward details, borewell details, water-level charts, and discharge charts.
- Allows filtering by data availability.
- Allows CSV export for the selected borewell or filtered data, depending on the current UI setup.

---

## Project Structure

```text
.
├── index.html
├── BBMP_Dashboard.css
├── bbmpwards.zip
└── README.md
```

---

## Included Files

### `index.html`

Main dashboard page containing:

- Map initialization
- Sensor marker rendering
- Ward shapefile loading
- API calls to the backend
- Chart rendering
- Sidebar interactions
- CSV export logic

### `BBMP_Dashboard.css`

Stylesheet for the dashboard layout, map, sidebars, cards, buttons, legends, and charts.

### `bbmpwards.zip`

Bundled BBMP ward shapefile used to display ward boundaries on the map.

The shapefile ZIP should contain:

```text
.shp
.shx
.dbf
.prj
```

---

## Backend API

This frontend expects a backend API to be running separately.

Update the backend URL inside `index.html`:

```javascript
const API_BASE_URL = 'https://bbmp-borewell-backend.onrender.com';
```

The frontend expects these API routes:

```text
GET /api/sensors
GET /api/water-level?uid=<sensor_uid>
GET /api/status
GET /api/refresh
```

Example full API calls:

```text
https://bbmp-borewell-backend.onrender.com/api/sensors
https://bbmp-borewell-backend.onrender.com/api/water-level?uid=<sensor_uid>
```

---

## Important Security Note

Do **not** store sensitive data in this frontend repository.

Do not commit:

```text
KH credentials
database URLs
API secrets
raw KH downloaded data
data_sent_from_kh/
.env files
backend Python scripts
private CSV/XLSX files
```

This frontend repository should contain only public static files required to display the dashboard.

Sensitive downloading, parsing, storage, and authentication must be handled by the backend.

---

## Deployment on GitHub Pages

1. Push this repository to GitHub.

2. Go to:

```text
Repository → Settings → Pages
```

3. Set:

```text
Source: Deploy from a branch
Branch: main
Folder: / root
```

4. Save.

5. GitHub Pages will publish the dashboard at:

```text
https://VishwasPrabhakara.github.io/bbmp-borewell-dashboard/
```

---

## Required Frontend Files

Before deploying, make sure the repo contains:

```text
index.html
BBMP_Dashboard.css
bbmpwards.zip
README.md
```

The `bbmpwards.zip` file must be in the same directory as `index.html` because the dashboard loads it using:

```javascript
fetch('bbmpwards.zip')
```

---

## Features

### Interactive Map

- OpenStreetMap basemap
- BBMP ward boundary overlay
- Borewell sensor markers
- Clickable ward polygons
- Clickable sensor markers

### Borewell Details

Clicking a borewell displays:

- UID
- Ward number
- Ward name
- Latitude and longitude
- First available data date
- Last available data date
- Reading count
- Data type

### Charts

The right-side panel displays:

- Water-level chart
- On-level and off-level lines, when available
- Discharge chart, when discharge data is available
- Hover tooltips with units such as `ft` and `L/min`

### Time Filters

Available chart filters:

- Last Week
- Last Month
- 3 Months
- All Time

### Layout

- Collapsible left sensor list
- Collapsible right details/chart panel
- Responsive map layout

---

## Data Flow

```text
GitHub Pages frontend
        ↓
Render backend API
        ↓
Database / processed KH data
```

The frontend does not directly download KH data and does not connect directly to the database.

---

## Notes

This repository is only for the static dashboard interface.

The backend service is responsible for:

- KH data download
- Data cleaning and parsing
- Database storage
- API response generation
- Scheduled refresh jobs
