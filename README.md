# Orbital Contact Analyzer

![Image](https://github.com/user-attachments/assets/4912f8a8-bda7-45f5-b553-202cbc485017)

A single-file, offline web application for simulating two Earth satellites and a ground station. The application renders 2D/3D views, visualizes sensor footprints, and computes satellite-to-satellite line-of-sight (LOS) and satellite-to-ground-station access intervals.

This tool is designed as an educational platform to demonstrate core orbital mechanics concepts in an interactive way.

---

## Key Features

*   **2D Map & 3D Globe:** Toggle between an equirectangular map and a full 3D WebGL globe.
*   **J2 Perturbation Model:** Includes J2 secular effects on RAAN (Ω) and Argument of Perigee (ω) for more realistic long-term orbit precession.
*   **Interactive Visualizations:** View ground tracks, sensor footprints (FOV), local horizons, and communication links.
*   **Contact Analysis:** Automatically calculates and tables all line-of-sight (LOS) windows between satellites and access times from a ground station.
*   **Data Export:** A single click exports all computed contact data to a CSV file.
*   **Fully Offline:** Runs entirely in your browser with no external network access required. All logic is self-contained in the HTML file.
*   **Physically Correct Inertial View:** The 3D view can fix the orbital planes in space to correctly show the Earth rotating underneath.

## How to Run

No installation is needed. This is a single-file application.

1.  Download the `Orbital_Contact_Analyzer.html` file from this repository.
2.  Open the file in a modern desktop web browser (Chrome, Firefox, Edge, or Safari).

**System Requirements:**
*   A modern desktop browser with WebGL enabled.
*   8+ GB RAM is recommended for simulations with long timelines or small time steps.

## Purpose & Scope

This application is designed for first-order analysis, educational use, and demonstration. It prioritizes interactivity, speed, and the clear visualization of orbital mechanics concepts.

The simulation propagates two satellites and a ground station, converting positions between ECI (Earth-Centered Inertial) and ECEF (Earth-Centered Earth-Fixed) frames to drive the visuals and the core access calculations.

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

## License

This project is licensed under the **MIT License**. See the `LICENSE` file for details. You are free to modify, distribute, and use this software, even for commercial purposes, as long as you provide attribution.

## Contributing

Found a bug or have an idea for a new feature? Please open an issue in this repository.

## The Development Story

This application was developed in a unique collaboration between a human project manager and an AI coding partner (Gemini and GPT models). The AI authored the code, while the humans managed the project's scope, conducted reviews, and handled testing. You can read the full story of how it was built in this blog post: [An Educational Satellite Explorer—Built with AI](https://paulhenkiel.com/2025/10/21/two-satellite-explorer-footprints-los/).

## Acknowledgments

*   Thank you to **Jay** for invaluable ideas, feedback, and review throughout the project.
*   The 2D map and 3D globe textures are based on NASA Visible Earth's image set: ["Blue Marble: Land Surface, Shallow Water, and Shaded Topography."](https://visibleearth.nasa.gov/images/73751/blue-marble-land-surface-shallow-water-and-shaded-topography)
