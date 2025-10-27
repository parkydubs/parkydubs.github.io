---
layout: single
title: FlowerFit
date: 2025-08-10
toc: true
excerpt: "Flowers That Thrive, Communities That Flourish: a sustainability-focused web app that helps new gardeners choose plants suited to their local climate."
---

[Hackathon][project]{: .btn .btn--info}
[Repo][repo]{: .btn .btn--inverse}

## Overview

### Background

FlowerFit is a sustainability-driven web app I built to help new gardeners make informed and eco-friendly choices when selecting plants. The goal is to recommend flowers best suited to a user’s local climate while promoting biodiversity and environmental responsibility.

The interface was designed using **Tailwind CSS**, featuring an opaque overlay on a flower background image to keep the design visually appealing and readable. The app is simple, intuitive, and designed for all experience levels, from beginner gardeners to those exploring sustainable landscaping practices.

### Mission / Sustainable Goals

**Protecting Pollinators**  
FlowerFit recommends pollinator-friendly flowers, helping to restore habitats for bees, butterflies, and other vital pollinators.

**Reducing Garden Waste**  
By guiding users to plants that naturally thrive in their area, the app helps reduce garden waste and increases planting success rates.

**Fostering Biodiversity**  
The app promotes native species, encouraging gardeners to support local ecosystems and preserve biodiversity.

### User Flow / Functionality

**Location Input**  
Users can input their location or climate zone by either:

- Clicking a **“Use My Location”** button, which leverages the **Geolocation API** (and, in the demo version, returns a hardcoded zone), or
- Entering a **ZIP code** prefix (examples: `902`, `100`, `606`, `733`) and clicking **“Lookup”**.

**Zone Determination**  
The app determines the user’s **USDA Hardiness Zone**, which indicates the average winter low temperatures that plants can survive in. This zone forms the basis for flower recommendations.

**Flower Recommendation**  
Once the zone is identified, FlowerFit displays a curated list of flowers suitable for that specific region. Each flower entry includes:

- The **name** of the flower
- Its **color**
- Additional **notes** about its characteristics
- **Tags** such as _Pollinator-Friendly_ or _Native Plant_

**Color Scheme Suggestions**  
FlowerFit also generates sample aesthetic color palettes for inspiration. These include:

- **Complementary** color schemes
- **Analogous** color schemes
- **Dominant / Secondary / Accent** combinations

### Interface Design

The layout uses **Tailwind CSS** for styling and responsiveness. I incorporated an opaque overlay over the background flower image to improve contrast and legibility. Buttons, grids, and cards use Tailwind’s utility classes (e.g., `md:grid-cols-3`) for clean, modern design.

---

## Technology & Tools

### Languages

- **HTML:** Provides the structure and layout for the page
- **CSS / Framework:** Uses **Tailwind CSS** for utility-first styling, quick prototyping, and responsive design. Custom CSS was added for the background image and button shadows.
- **JavaScript:** Handles the app’s core logic, including event handling, location retrieval, flower list generation, and color palette creation.

### Backend Logic (Simulated for Demo)

- **Data Mapping:**  
  A JavaScript object `zipToZone` simulates a ZIP code–to–zone lookup by mapping 3-digit prefixes (e.g., `'902' → '10b'`).
- **Data Structure:**  
  A `zoneFlowers` object stores sample flower data, organized by hardiness zone (e.g., `'10b'` includes Sunflower, `'8b'` includes Texas Bluebonnet).
- **Geolocation:**  
  The app uses `navigator.geolocation.getCurrentPosition` to retrieve the user’s location. In the demo version, it returns a hardcoded zone (`'7b'`) for simplicity.

---

## References

- **USDA Plant Hardiness Zone Map** — [https://planthardiness.ars.usda.gov](https://planthardiness.ars.usda.gov)  
  (Used for understanding climate zones and referencing accurate regional planting information.)

---

[project]: #
[repo]: #
