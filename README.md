# Orbital Contact Analyzer
**Current Version:** 1.3.0

![Image](https://github.com/user-attachments/assets/5959ceea-4c6e-4665-add9-e1e4a1e0ea19)

## Live Demo

**This application is live and can be used directly in your browser.**

**➡️ [Launch Orbital Contact Analyzer](https://henkielp.github.io/Orbital-Contact-Analyzer/)**


A single-file, offline web application for simulating two Earth satellites and up to two ground stations. The application renders 2D/3D views, visualizes sensor footprints, and computes satellite-to-satellite line-of-sight (LOS) and satellite-to-ground-station access intervals.

This tool is designed as an educational platform to demonstrate core orbital mechanics concepts in an interactive way.

---

## Key Features

*   **2D Map & 3D Globe:** Toggle between an equirectangular map and a full 3D WebGL globe.
*   **J2 Perturbation Model:** Includes J2 secular effects on RAAN (Ω) and Argument of Perigee (ω) for more realistic long-term orbit precession.
*   **Interactive Visualizations:** View ground tracks, sensor footprints (FOV), local horizons, and communication links.
*   **Dual Ground Stations:** Configure up to two independent ground stations, each with its own coordinates and elevation mask. GS1 is shown as a white triangle, GS2 as a green triangle.
*   **Contact Analysis:** Automatically calculates and tables all line-of-sight (LOS) windows between satellites and access times from both ground stations.
*   **Data Export:** A single click exports all computed contact data to a CSV file.
*   **Fully Offline:** Runs entirely in your browser with no external network access required. All logic is self-contained in the HTML file.
*   **Physically Correct Inertial View:** The 3D view can fix the orbital planes in space to correctly show the Earth rotating underneath.

## How to Run

No installation is needed. This is a single-file application.

1.  Download the index.html file from this repository.
2.  Open the file in a modern desktop web browser (Chrome, Firefox, Edge, or Safari).

## Documentation

A complete user manual is available for detailed instructions on all features, controls, and workflows.

**➡️ [Read the Full User Manual Here](User-Manual.html)**


**System Requirements:**
*   A modern desktop browser with WebGL enabled.
*   8+ GB RAM is recommended for simulations with long durations or small time steps.

## Purpose & Scope

This application is designed for first-order analysis, educational use, and demonstration. It prioritizes interactivity, speed, and the clear visualization of orbital mechanics concepts.

The simulation propagates two satellites and up to two ground stations, converting positions between ECI (Earth-Centered Inertial) and ECEF (Earth-Centered Earth-Fixed) frames to drive the visuals and the core access calculations.

## Limitations

This is an educational tool, not a validated, mission-critical analysis suite. It makes several simplifying assumptions:

#### The Model **INCLUDES**:
*   **J2 Perturbations:** Models the long-term precession of the orbit due to Earth's equatorial bulge.
*   **Spherical Earth:** Assumes a perfect sphere for all ground geometry, occlusion checks, and footprint calculations.

#### The Model **DOES NOT INCLUDE**:
*   **Atmospheric Drag:** Orbits will not decay.
*   **Solar Radiation Pressure (SRP).**
*   **Third-Body Gravity:** Gravitational effects from the Moon, Sun, etc., are ignored.
*   **Higher-Order Gravity Fields.**
*   **Earth Oblateness (WGS-84):** Does not use a standard ellipsoid, which may introduce small errors in ground track positions.
*   **Terrain:** Access calculations do not account for terrain that could block visibility.

---

## Changelog

### v1.3.0
New feature release adding a second ground station:

*   **Ground Station 2:** A second independent ground station with its own latitude, longitude, and elevation mask. Disabled by default; enable via the "Show Ground Station 2" dropdown.
*   **Visual Distinction:** GS1 appears as a white triangle, GS2 as a green triangle on both the 2D map and 3D globe. Access link lines are drawn in each satellite's color.
*   **Merged Access Table:** The Ground Station Access Intervals table now includes a "Station" column (GS1 or GS2) and displays intervals from both stations in chronological order.
*   **Dual Footer Badges:** Separate real-time status badges for GS1 Access and GS2 Access in the footer bar.
*   **CSV Export:** Ground station intervals are now labeled `ground-station-1` or `ground-station-2` in the type column.
*   **Scenario Presets:** Loading a preset resets GS2 to disabled. Presets can optionally define a `gs2` field for dual-station scenarios.
*   **Code Cleanup:** Removed 176 lines of stray Evernote/Skitch CSS artifacts and a browser-injected comment that were captured during a previous file save.

### v1.2.0
New feature release adding TLE (Two-Line Element) import capability:

*   **TLE Import:** Parse standard Two-Line Element sets to automatically populate orbital elements for either satellite.
*   **Collapsible UI:** Each satellite panel includes a collapsible "Import from TLE" section.
*   **Epoch Sync Option:** Checkbox to optionally set the simulation epoch to match the TLE epoch.
*   **Epoch Mismatch Warning:** Alerts user when TLE epoch differs from simulation epoch by more than 1 day.
*   **TLE Epoch Display:** Shows the imported TLE's epoch for reference (visible when section is expanded).
*   **Orbit Validation:** Validates that the parsed orbit has perigee above Earth's surface.
*   **Keyboard Shortcuts:** `T` opens TLE import for Satellite 1, `Shift+T` for Satellite 2.

**Supported TLE format:**
```
ISS (ZARYA)             ← Optional name line
1 25544U 98067A   ...   ← Line 1 (epoch, drag terms)
2 25544  51.6400  ...   ← Line 2 (orbital elements)
```

**A note on TLE epochs:**

A TLE is a snapshot of a satellite's orbit at a specific moment in time (the "epoch"). Think of it like a photograph: it shows exactly where the satellite was and how it was moving at that instant.

If you import two TLEs with different epochs and run them from the same simulation start time, one satellite will be in the wrong position. For example, if Satellite 1's TLE is from January 15th and Satellite 2's TLE is from January 20th, but your simulation starts on January 15th, then Satellite 2 will appear where it *would have been* on January 20th, not where it *actually was* on January 15th.

For best results, use TLEs with epochs within a day of each other, or enable "Set simulation epoch to TLE epoch" for one satellite and accept that the other may have some position error.

Also note: some TLE sources "normalize" their data so satellites always start at the equator (ascending node). Raw TLEs from [CelesTrak](https://celestrak.org) or [Space-Track](https://space-track.org) show satellites at their actual positions. See the User Manual for more details.

### v1.1.2
New feature release adding keyboard shortcuts for improved workflow:

| Key | Action |
|-----|--------|
| `Space` | Play/Pause simulation |
| `R` | Reset to start |
| `←` / `→` | Step backward/forward (auto-pauses) |
| `V` | Toggle 2D/3D view |
| `I` | Toggle Inertial view (3D only) |
| `0` | Free camera (no focus) |
| `1` | Focus on Satellite 1 |
| `2` | Focus on Satellite 2 |
| `E` | Export CSV |
| `T` | Open TLE import for Satellite 1 |
| `Shift+T` | Open TLE import for Satellite 2 |

*Note: Shortcuts are disabled when typing in input fields.*

### v1.1.1
Bug fix release addressing numerical edge cases and code quality improvements:

*   **Fixed negative longitude wrapping:** Corrected the `wrapLon` function to properly handle negative longitudes using JavaScript's modulo behavior.
*   **Fixed negative angle wrapping:** Corrected the `wrapPi` function for proper angle normalization with negative values.
*   **Fixed 90° elevation mask edge case:** Added numerical tolerance (`GS_EL_EPS`) and domain clamping to prevent `NaN` results when ground station elevation mask is set to exactly 90°.
*   **Removed dead UI references:** Cleaned up undefined `ui.map2DStyle` and unified terminator toggle handling.
*   **Improved code clarity:** Renamed internal True Anomaly variables from `M` to `nu` for semantic correctness (Mean Anomaly is conventionally `M`, True Anomaly is `ν`).

### v1.1.0
*   Initial public release with J2 perturbations, dual satellite simulation, ground station access, and 2D/3D visualization.

---

## License

This project is licensed under the **MIT License**. See the `LICENSE` file for details. You are free to modify, distribute, and use this software, even for commercial purposes, as long as you provide attribution.

## Contributing

Found a bug or have an idea for a new feature? Please open an issue in this repository.

## The Development Story

This application was developed in a unique collaboration between a human project manager and an AI coding partner (Gemini and GPT models). The AI authored the code, while the humans managed the project's scope, conducted reviews, and handled testing. You can read the full story of how it was built via the original post on my website or the offline copy archived with this repository:

*   **Original Blog Post (Live):** [An Educational Satellite Explorer—Built with AI](https://henkiel.com/2025/10/21/two-satellite-explorer-footprints-los/)
*   **Archived Version (Offline):** [An Educational Satellite Explorer—Built with AI](docs/development-story.html)

## Acknowledgments

*   Thank you to **Jay** for invaluable ideas, feedback, and review throughout the project.
*   The 2D map and 3D globe textures are based on NASA Visible Earth's image set: ["Blue Marble: Land Surface, Shallow Water, and Shaded Topography."](https://visibleearth.nasa.gov/images/73751/blue-marble-land-surface-shallow-water-and-shaded-topography) For similar imagery, see NASA's ["Blue Marble: Next Generation Base Map with Topography."](https://science.nasa.gov/earth/earth-observatory/blue-marble-next-generation/base-topography/)
