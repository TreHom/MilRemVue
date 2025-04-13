# Milrem intership test project
Milrem software internship applications home project with the goal of developing an interface prototype for an UGV employing Vue 3 alongside HTML, CSS, and TypeScript.


## Features

- Interactive map interface using Leaflet
- Vehicle position tracking and movement controls
- Waypoint management system
  - Add waypoints with long-press on map
  - Name and save waypoints
  - View waypoints in a list
  - Drive to waypoints
  - Delete waypoints
- Engine status control
- Movement controls with engine status validation

## Prerequisites

- Node.js (v14 or higher)
- npm (v6 or higher)

## Installation

1. Clone the repository:
```bash
git clone [your-repository-url]
cd MilRemVue
```

2. Install dependencies:
```bash
npm install
```

## Project Setup

The project uses the following main dependencies:
- Vue 3
- Leaflet for map functionality
- Vue-Leaflet for Vue integration with Leaflet

## Development

To run the development server:

```bash
npm run serve
```

This will start the development server at `http://localhost:8080` (or another available port if 8080 is in use).


## Component Overview

### MapApplication
- Displays the main map interface
- Handles waypoint placement and management
- Shows vehicle position

### MovementControls
- Provides directional controls (↑, ↓, ←, →)
- Validates engine status before movement
- Shows popup when engine is off

### EngineStart
- Controls vehicle engine status
- Displays current engine state

### WaypointList
- Displays saved waypoints
- Allows waypoint management (delete, rename, drive to)

### WaypPint
- Implements the waypoint
- ALlows waypoint managment (add waypoint, move vehicle, discard)

### VehicleMarker
- Displays a generic waypoint marker for the ugv location

## Usage

1. Start the application using `npm run serve`
2. The map interface will display with the vehicle at the initial position
3. Use the engine control to start/stop the engine
4. Use movement controls to navigate the vehicle
5. Long-press on the map to create waypoints, this creates a temporary map marker
6. Click on the temporary marker to add waypoints
7. Manage waypoints using the waypoint list