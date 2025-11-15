# Ireland Hotels — Hotel Booking Intelligence Dashboard

[**Live Website**](https://ireland-hotels-dineshbarri.netlify.app/)

---

> **One-line summary:** Interactive dashboard for exploring Ireland hotel prices, ratings, and availability (focused on weekend-night stays). Built as a fully responsive, front-end visual analytics site using maps, charts, filters, and an image gallery.

---

## 📌 Table of Contents
- [Project Overview](#project-overview)
- [Live Demo](#live-demo)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Repository Structure](#repository-structure)
- [Data Handling](#data-handling)
- [Local Setup](#local-setup)
- [Using Real Booking Data](#using-real-booking-data)
- [Design & Implementation Notes](#design--implementation-notes)
- [DAX Examples](#dax-examples)
- [Screenshots](#screenshots)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License & Scraping Ethics](#license--scraping-ethics)
- [Author](#author)

---

## 🔍 Project Overview
This dashboard visualizes hotel listings in Ireland with a special focus on **weekend-night pricing**. It integrates an interactive map, dynamic charts, hotel filters, and a gallery to provide a full visual exploration environment.

⚠️ **Note:** The project currently uses **generated sample data** from `main.js` (for demo purposes). It is fully engineered to accept real scraped/API-fed data when available.

---

## 🌐 Live Demo
View the fully deployed site here:
👉 **https://ireland-hotels-dineshbarri.netlify.app/**

---

## ⭐ Key Features
- 🗺️ **Interactive Leaflet Map** with clustering & popups
- 📊 **ECharts visualizations**: pricing, ratings, distribution, trends
- 🔎 **Filters**: city, price range, rating, room type, policies (breakfast, cancellation)
- 🏨 **Hotel detail cards** with comparison view
- 🎞️ **Image gallery & animated UI elements**
- 📱 **100% responsive layout** (desktop/tablet/mobile)
- 🔧 **Synthetic data generator** for offline demo (400+ hotels simulated)
- 📘 **Design docs included**: design.md, implementation.md, interaction.md, outline.md

---

## 🛠️ Tech Stack
**Frontend:** HTML5, CSS3, JavaScript  
**Libraries:**
- 📌 Leaflet.js (maps)
- 📌 ECharts (charts)
- 📌 Anime.js (animations)
- 📌 Typed.js (typing animations)
- 📌 Splide.js (image carousel)
- 📌 Tailwind CSS (utility styling via CDN)

No build step required — **static site**.

---

## 📁 Repository Structure
```
/
├── index.html               # Main dashboard
├── style.css                # Dashboard styling
├── main.js                  # Charts, map rendering, data generator
├── package.json             # Minimal metadata
│
├── design.md                # Design system + color palette
├── implementation.md        # Implementation notes + DAX samples
├── interaction.md           # Interaction / UX details
├── outline.md               # Project outline & plan
│
└── resources/               # Images & assets
    ├── hero-bg.jpg
    ├── hotel-1.jpg
    ├── hotel-2.jpg
    ├── hotel-3.jpg
    └── hotel-4.jpg
```

---

## 🗄️ Data Handling
The dashboard expects hotel objects of this form:
```js
{
  id: Number,
  name: String,
  city: String,
  price: Number,
  score: Number,
  reviews: Number,
  room_type: String,
  rooms_left: Number,
  free_cancellation: Boolean,
  breakfast_included: Boolean,
  lat: Number,
  lng: Number
}
```
`main.js` currently generates **synthetic data** via `generateSampleData()`.

---

## 💻 Local Setup
Clone the repo:
```bash
git clone <repo-url>
cd <repo-folder>
```
Start a simple local server:
```bash
python -m http.server 8000
```
Open:
```
http://localhost:8000
```

---

## 🔄 Using Real Booking Data
> ⚠️ Always follow Booking.com Terms of Service.  
> Prefer APIs or licensed data sources.

### **Option A — Local JSON File**
Save your scraped API data to:
```
data/hotels.json
```
Modify `loadHotelData()`:
```js
async function loadHotelData() {
  const res = await fetch('data/hotels.json');
  hotelData = await res.json();
  filteredData = [...hotelData];
}
```

### **Option B — Backend API**
Your backend exposes:
```
/api/hotels?date=YYYY-MM-DD
```
Then:
```js
async function loadHotelData() {
  const res = await fetch('https://yourapi.com/api/hotels?date=2025-11-15');
  hotelData = await res.json();
  filteredData = [...hotelData];
}
```

### **Scraping Architecture (High-Level)**
- Use Playwright/Puppeteer for interactive pages  
- Extract:
  - Names, prices, reviews, score
  - Location, images, room types
  - Policies (breakfast, cancellation)
- Normalize JSON → store in DB → serve via API → dashboard consumes

---

## 🎨 Design & Implementation Notes
Summaries from `design.md`:
- Primary colors: **Deep Teal (#2C5F5D)**, **Warm Gold (#D4AF37)**
- Card components with shadows, metric banners, and chart containers
- Interaction patterns include filters, toggles, map + chart synchronization

From `implementation.md`:
- DAX logic samples for analytics
- Suggestions for BI pipeline integrations

---

## 📘 DAX Examples
Example metric (from documentation):
```dax
Total Revenue Potential = SUMX(
    Hotels,
    Hotels[price] * (Hotels[rooms_left] + CALCULATE(
        SUM(Bookings[rooms_booked]),
        Bookings[hotel_id] = Hotels[id]
    ))
)
```
See full details in `implementation.md`.

---

## 🖼️ Screenshots
Add images like:
```md
![Hero](resources/hero-bg.jpg)
```
(Images stored in `/resources/`)

---

## 📅 Roadmap
- Integrate live API / scraper pipeline  
- Add heatmap visualization for pricing  
- Add account logins and saved searches  
- Build CSV/Excel/PDF export  
- Add automated deployment & CI pipeline  
- Multi-language support + accessibility improvements

---

## 🤝 Contributing
1. Fork this repo  
2. Create a feature branch  
3. Submit a Pull Request with description and screenshots

Please open an issue before proposing scraper additions.

---

## ⚖️ License & Scraping Ethics
**License:** MIT (recommended)

**Scraping Policy:**
- Check target site ToS  
- Respect `robots.txt`  
- Avoid heavy automated scraping  
- Prefer APIs and partnerships  
- Avoid personal data exposure

---

## 👤 Author
**Dinesh Barri**  
**Live Dashboard:** https://ireland-hotels-dineshbarri.netlify.app/

If you'd like, I can also generate:
- `LICENSE` file (MIT)  
- `CONTRIBUTING.md`  
- Starter scraper (Python/Playwright or JS/Puppeteer)
