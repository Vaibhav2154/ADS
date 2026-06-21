# How to Add More Drones and Humans to the Simulation

This guide explains how to add new drone agents and scale the number of humans in both the **Multi-Drone Distributed System** and the **Single-Drone Simulation**.

---

## 🛰️ 1. Adding More Drones (Multi-Drone Mode)

To add a new drone (e.g., `D4`), you need to register it in the backend coordinate region system and update the frontend HTML files (Client and Admin) to display its marker and status.

### Step 1: Update Server Region Boundaries
Open [multi_drone_server.py](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/multi_drone_server.py) and update the `self.regions` dictionary in the `__init__` constructor. You need to assign the new drone ID (`D4`) its search region boundaries.

For example, to split the world size (800x800, coordinates range from `-400` to `400` on X and Z axes):

```python
# 3D-Simulation/multi_drone_server.py (around line 18)
self.regions = {
    "D1": {"x_from": -400, "x_to": 0, "z_from": -400, "z_to": 0},      # Bottom-left
    "D2": {"x_from": 0, "x_to": 400, "z_from": -400, "z_to": 0},       # Bottom-right  
    "D3": {"x_from": -400, "x_to": 0, "z_from": 0, "z_to": 400},       # Top-left (modified)
    "D4": {"x_from": 0, "x_to": 400, "z_from": 0, "z_to": 400}         # Top-right (NEW drone)
}
```

> [!NOTE]
> The server's human generator (`generate_humans()`) automatically generates humans for each region defined in `self.regions`. Adding `"D4"` will automatically spawn humans specifically within D4's region boundaries!

---

### Step 2: Add Drone Markers in the Client Map
Open [multi_drone_client.html](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/multi_drone_client.html) to style and declare the marker element for the new drone.

1. **Add style rules** for `.mini-drone-d4` inside `<style>` (around line 140):
   ```css
   .mini-drone-d4 { background-color: #ffd93d; } /* Choose a distinct color */
   ```

2. **Declare the marker element** inside `#mini-world-map` (around line 254):
   ```html
   <!-- Drone Markers -->
   <div class="mini-drone-marker mini-drone-d1" id="mini-drone-d1"></div>
   <div class="mini-drone-marker mini-drone-d2" id="mini-drone-d2"></div>
   <div class="mini-drone-marker mini-drone-d3" id="mini-drone-d3"></div>
   <div class="mini-drone-marker mini-drone-d4" id="mini-drone-d4"></div> <!-- NEW marker -->
   ```

---

### Step 3: Add Drone Panels and Markers in the Admin Dashboard
Open [admin_dashboard.html](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/admin_dashboard.html) and add the new drone's HTML layout, CSS styles, and JavaScript configs.

1. **Add CSS marker color** in the `<style>` block (around line 94):
   ```css
   .drone-d4 { background-color: #ffd93d; }
   ```

2. **Add region boundary visualization** (optional) in `<style>` (around line 113) and inside the map container (around line 125):
   ```css
   .region-d4 {
       top: 0;
       right: 0;
       width: 50%;
       height: 50%;
   }
   ```
   ```html
   <div class="region-boundary region-d4"></div>
   ```

3. **Declare the sidebar card** inside `#drone-list` (around line 298):
   ```html
   <div class="drone-info">
       <div>
           <h4>D4 - Top Right</h4>
           <p>Status: <span class="status-indicator status-offline"></span>Offline</p>
           <p>Position: [0, 0, 0]</p>
       </div>
   </div>
   ```

4. **Register the drone ID** in the JavaScript config list inside `updateDroneStatus()` (around line 414):
   ```javascript
   const droneConfigs = [
       { id: 'D1', name: 'D1 - Bottom Left', region: 'Bottom Left' },
       { id: 'D2', name: 'D2 - Bottom Right', region: 'Bottom Right' },
       { id: 'D3', name: 'D3 - Top Region', region: 'Top Region' },
       { id: 'D4', name: 'D4 - Top Right', region: 'Top Right' } // NEW drone
   ];
   ```

---

## 👥 2. Scaling Humans in the Simulation

### Scenario A: Increasing Human Count in Multi-Drone Mode
By default, the server generates **3 humans per drone region**. To increase this density (e.g., to 5 humans per region):

1. Open [multi_drone_server.py](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/multi_drone_server.py).
2. Find the loop inside `generate_humans()` (around line 36):
   ```python
   for region_id, region in self.regions.items():
       region_humans = []
       for i in range(5):  # Changed from range(3) to range(5)
   ```
3. Save the file and restart `multi_drone_server.py`. The server will now spawn and track 5 humans in each of the region sectors.

---

### Scenario B: Adding Specific Human Spawns in Single-Drone Mode
In single-drone mode (e.g., loading [index.html](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/index.html)), human locations are defined as static coordinates inside [index.js](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/index.js).

1. Open [index.js](file:///home/vaibhi/Dev/35-MAHAKUMBH-46bf24daad4130a9edf4d09570cc2ddf35d8842a/3D-Simulation/index.js) and locate the `HUMAN_LOCATIONS` constant (around line 66):
   ```javascript
   const HUMAN_LOCATIONS = [
     [85, 45],   // Coordinates for Alice [x, z]
     [-40, 110], // Coordinates for Bob [x, z]
     [60, 150],  // Coordinates for Charlie [x, z]
     [-120, -50] // NEW: Coordinates for David [x, z]
   ];
   ```

2. Register the corresponding name and detection type in `humanNames` and `humanModelTypes` arrays:
   ```javascript
   const humanNames      = ["Alice", "Bob", "Charlie", "David"];
   const humanModelTypes = ["image", "thermal", "audio", "image"];
   ```

3. Save the file and reload your single-drone client web page with a hard refresh.
