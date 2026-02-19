# Capstone Project — The Battle of the Neighborhoods
### IBM Data Science Professional Certificate · Coursera

> **Analyzing the distribution of fitness and sport facilities across Frankfurt am Main to identify optimal locations for a new gym business.**

---

## Overview

This capstone project applies a full data science pipeline to a real-world business question: **Where should an investor open a new Fitness Center or Gym in Frankfurt, Germany?**

Using location data from the **Google Places API**, web scraping, geospatial analysis, and unsupervised machine learning, the project maps existing sport venues across all Frankfurt boroughs, clusters neighborhoods by similarity, and surfaces underserved areas with high business potential.

---

## Repository Structure

```
.
├── Capstone_The-Battle-of-the-Neighborhoods.ipynb   ← Main analysis notebook
├── README.md                                         ← This file
├── requirements.txt                                  ← Python dependencies
└── assets/
    ├── venues_per_borough.png                        ← Venue count bar chart
    ├── avg_rating_per_borough.png                    ← Google rating bar chart
    └── elbow_plot.png                                ← KMeans elbow curve
```

---

## Methodology

| Step | Description |
|------|-------------|
| **1. Data Collection** | Scrape Frankfurt borough list from Wikipedia using `requests` + `BeautifulSoup` |
| **2. Geocoding** | Obtain latitude/longitude for each borough via Nominatim (OpenStreetMap) with rate limiting |
| **3. API Queries** | Fetch fitness venue data from **Google Places Nearby Search API** per borough centroid, with pagination (up to 60 results per borough) |
| **4. Feature Engineering** | One-hot encode venue categories; compute mean frequency per borough |
| **5. Clustering** | Apply KMeans with elbow-method cluster selection; `StandardScaler` applied before fitting |
| **6. Visualization** | Interactive Folium maps with GeoJSON overlays; matplotlib charts including Google ratings |

---

## Why Google Places API?

| Feature | Google Places | Foursquare v3 |
|---------|--------------|---------------|
| Coverage in Germany | ⭐⭐⭐⭐⭐ Excellent | ⭐⭐⭐ Good |
| Star ratings & reviews | ✅ Yes | ✅ Yes |
| Pagination (60 results/borough) | ✅ Yes | ❌ No |
| Price level data | ✅ Yes | ❌ No |
| Opening hours | ✅ Yes | Limited |
| Free tier | $200/month credit | 1,000 req/day |
| API key required | ✅ Yes | ✅ Yes |

---

## Key Findings

- The **city centre** (Innenstadt I–III) and **Bornheim/Ostend** have the highest concentration of fitness venues — highly competitive markets.
- The southern borough **Süd** (including the airport area) is significantly underserved relative to its population, making it the strongest candidate for a new facility.
- Top venue categories across Frankfurt: **Gym**, **Fitness Studio**, **Yoga Studio**.
- Google ratings reveal a quality dimension beyond simple venue counts — some boroughs with fewer venues show higher average ratings, indicating premium demand.
- KMeans clustering groups the boroughs into 10 distinct fitness-venue profiles, enabling targeted business strategy.

---

## Tech Stack

| Category | Libraries / Services |
|----------|----------------------|
| Data manipulation | `pandas >= 2.0`, `numpy` |
| Web scraping | `requests`, `beautifulsoup4`, `lxml` |
| Geocoding | `geopy` (Nominatim + RateLimiter) |
| Venue data | **Google Places API** (Nearby Search) |
| Machine learning | `scikit-learn` (KMeans, StandardScaler) |
| Visualization | `matplotlib`, `folium`, `folium.plugins.MarkerCluster` |

> **Python 3.12 compatible.** Uses `n_init="auto"` for KMeans, `pd.read_html(response.text)` to bypass Wikipedia blocking, and pre-fetched GeoJSON dicts to fix VS Code iframe rendering.

---

## Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/your-username/battle-of-neighborhoods-frankfurt.git
cd battle-of-neighborhoods-frankfurt
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Get a Google Places API key

1. Go to [https://console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project
3. Navigate to **APIs & Services → Library**
4. Search for and enable **Places API**
5. Go to **APIs & Services → Credentials → Create Credentials → API Key**
6. Copy the key and paste it into the notebook:

```python
GOOGLE_API_KEY = "YOUR_GOOGLE_API_KEY_HERE"
```

> **Free tier:** Google provides $200/month in free credit, which covers approximately 5,000 Nearby Search requests — more than enough for this project.

### 4. Run the notebook
```bash
jupyter notebook Capstone_The-Battle-of-the-Neighborhoods.ipynb
```

---

## Data Sources

| Source | Usage |
|--------|-------|
| [Wikipedia — Frankfurt Ortsbezirke](https://de.wikipedia.org/wiki/Liste_der_Ortsbezirke_von_Frankfurt_am_Main) | Borough names and neighborhood structure |
| [Nominatim / OpenStreetMap](https://nominatim.org/) | Borough geocoordinates |
| [Google Places API — Nearby Search](https://developers.google.com/maps/documentation/places/web-service/search-nearby) | Fitness & sport venue listings with ratings |
| [Frankfurt Open Data — GeoJSON](https://offenedaten.frankfurt.de/) | District boundary polygons for map overlays |

---

## requirements.txt

```
pandas>=2.0
numpy>=1.26
requests>=2.31
beautifulsoup4>=4.12
lxml>=4.9
geopy>=2.4
scikit-learn>=1.4
matplotlib>=3.8
folium>=0.15
```

---

## License

This project was completed as part of the [IBM Data Science Professional Certificate](https://www.coursera.org/professional-certificates/ibm-data-science) on Coursera. For educational use only.
