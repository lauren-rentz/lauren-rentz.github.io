---
layout: page
title: Portfolio
permalink: /portfolio/
header: no
---

Welcome to my portfolio! Here you will find a selection of my coursework and computational projects, demonstrating my ability to apply kinesiology and biomechanical concepts to real-world data and technology.

### Table of Contents
- [Research Papers and Reviews](#research-papers-and-reviews)
- [Data Analysis & Modeling](#data-analysis--modeling)
- [Data Organization and Visualization](#data-organization-and-visualization)
- [Video Analysis](#video-analysis)

---

## Research Papers and Reviews

- **[TrainingPeaks App Review](/assets/documents/App_Review_TrainingPeaks.pdf)**
  A comprehensive review of the TrainingPeaks application from a kinesiology and sports science perspective.
- **[KNES 381 Final Paper](/assets/documents/KNES381FinalPaper_LaurenRentz.docx)**
  My final review and analysis paper for KNES 381, highlighting the current use of AI in the rehabilitation of knee injuries.

## Data Analysis & Modeling

- **[Realistic Athlete Performance Data](/assets/documents/realistic_athlete_performance_revised.xlsx)**
  An Excel spreadsheet used to model and graph athlete performance metrics.
- **[Computational Analysis Notebook](/assets/documents/my-demo2-notebook.html)**
  A snippet from one of my Jupyter notebooks demonstrating my data analysis capabilities using Python. This page has been converted to html for better webpage readability.

## Video Analysis

A crucial aspect of sports science is understanding human movement through detailed motion analysis. The following images are excerpts from my video analysis projects tracking specific movement patterns in cross country skiers :

![Video Analysis Frame 1](/images/portfolio/videoanalysis1.png)

![Video Analysis Frame 2](/images/portfolio/videoanalysis2.png)

![Video Analysis Frame 3](/images/portfolio/videoanalysis3.png)

![Video Analysis Frame 4](/images/portfolio/videoanalysis4.png)

![Video Analysis Frame 5](/images/portfolio/videoanalysis5.png)

## Data Organization and Visualization

Here are some of my recent long-distance races mapped out natively on the site, compiled onto one map for easy viewing. I extracted the coordinates from the original Garmin `.fit` files spanning half-marathons to 5k races, and rendered them interactively using GPS data processing and Leaflet.js mapping!

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin=""/>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin=""></script>

<div id="stravaMap" style="height: 480px; width: 100%; border-radius: 8px; margin-top: 20px; z-index: 1;"></div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    var map = L.map('stravaMap').setView([51.0447, -114.0719], 10);
    
    L.tileLayer('https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png', {
      maxZoom: 19,
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>'
    }).addTo(map);

    var files = [
      { url: '/assets/data/Servus_Credit_Union_Marathon.geojson', color: '#e74c3c' },
      { url: '/assets/data/Dino_Dash_5k_.geojson', color: '#2980b9' },
      { url: '/assets/data/Last_Chance_Half_Marathon.geojson', color: '#27ae60' }
    ];

    var bounds = L.latLngBounds();
    var loaded = 0;

    files.forEach(function(file) {
      fetch(file.url)
        .then(res => res.json())
        .then(data => {
            var layer = L.geoJSON(data, {
                style: { color: file.color, weight: 4, opacity: 0.8 }
            }).addTo(map);
            bounds.extend(layer.getBounds());
            loaded++;
            if (loaded === files.length) {
                map.fitBounds(bounds, { padding: [20, 20] });
            }
        })
        .catch(err => console.error("Could not load " + file.url, err));
    });
  });
</script>
