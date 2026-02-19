# Capstone Project — The Battle of the Neighborhoods
### IBM Data Science Professional Certificate · Coursera

> **Analyzing the distribution of fitness and sport facilities across Frankfurt am Main to identify optimal locations for a new gym business.**

---

## Overview

This capstone project applies a full data science pipeline to a real-world business question: **Where should an investor open a new Fitness Center or Gym in Frankfurt, Germany?**

Using location data, web scraping, geospatial analysis, and unsupervised machine learning, the project maps existing sport venues across all Frankfurt boroughs, clusters neighborhoods by similarity, and surfaces underserved areas with high business potential.

---

## Repository Structure

```
.
├── Capstone_The-Battle-of-the-Neighborhoods.ipynb   ← Main analysis notebook
├── README.md                                         ← This file
├── requirements.txt                                  ← Python dependencies
└── assets/
    ├── venues_per_borough.png                        ← Bar chart output
    └── elbow_plot.png                                ← KMeans elbow curve
```

---

## Methodology

| Step | Description |
|------|-------------|
| **1. Data Collection** | Scrape Frankfurt borough list from Wikipedia using `requests` + `BeautifulSoup` |
| **2. Geocoding** | Obtain latitude/longitude for each borough via Nominatim (OpenStreetMap) with rate limiting |
| **3. API Queries** | Fetch fitness venue data from Foursquare Places API v3 per borough centroid |
| **4. Feature Engineering** | One-hot encode venue categories; compute mean frequency per borough |
| **5. Clustering** | Apply KMeans with elbow-method cluster selection; `StandardScaler` applied before fitting |
| **6. Visualization** | Interactive Folium maps with GeoJSON overlays; matplotlib charts |

---

## Key Findings

- The **city centre** (Innenstadt I–III) and **Bornheim/Ostend** have the highest concentration of fitness venues — highly competitive markets.
- The southern borough **Süd** (including the airport area) is significantly underserved relative to its population, making it the strongest candidate for a new facility.
- Top venue categories across Frankfurt: **Gym**, **Fitness Studio**, **Yoga Studio**.
- KMeans clustering groups the 46 boroughs into 10 distinct fitness-venue profiles, enabling targeted business strategy.

---

## Tech Stack

| Category | Libraries |
|----------|-----------|
| Data manipulation | `pandas >= 2.0`, `numpy` |
| Web scraping | `requests`, `beautifulsoup4`, `lxml` |
| Geocoding | `geopy` (Nominatim + RateLimiter) |
| Machine learning | `scikit-learn` (KMeans, StandardScaler) |
| Visualization | `matplotlib`, `folium`, `folium.plugins.MarkerCluster` |
| API | Foursquare Places API **v3** |

> **Python 3.12 compatible.** All deprecated patterns (conda installs, FSQ v2 endpoint, legacy `n_init` warnings, `pd.get_dummies` dtype changes) have been updated.

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

### 3. Add your Foursquare API key

Open the notebook and replace the placeholder in the credentials cell:
```python
FSQ_API_KEY = "YOUR_FOURSQUARE_API_KEY_HERE"
```
Get a free API key at [https://developer.foursquare.com](https://developer.foursquare.com).

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
| [Foursquare Places API v3](https://developer.foursquare.com/) | Fitness & sport venue listings |
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
