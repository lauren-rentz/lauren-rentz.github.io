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

- **<a href="https://view.officeapps.live.com/op/view.aspx?src=https://lauren-rentz.github.io/assets/documents/realistic_athlete_performance_revised.xlsx" target="_blank" rel="noopener noreferrer">Realistic Athlete Performance Data</a>**
  An Excel spreadsheet used to model and graph athlete performance metrics.
- **[Computational Analysis Notebook](/assets/documents/my-demo2-notebook.html)**
  A snippet from one of my Jupyter notebooks demonstrating my data analysis capabilities using Python. This page has been converted to html for better webpage readability.

## Video Analysis

A crucial aspect of sports science is understanding human movement through detailed motion analysis. The following images are excerpts from my video analysis projects tracking specific movement patterns in cross country skiers :

<details style="margin-bottom: 20px;">
  <summary style="cursor: pointer; padding: 12px; background-color: #f8f9fa; border: 1px solid #ddd; border-radius: 5px; font-weight: bold; user-select: none;">Click to View Video Analysis Frames</summary>
  <div style="padding: 15px 0;">

<img src="/images/portfolio/videoanalysis1.png" alt="Video Analysis Frame 1" style="width: 100%; margin-bottom: 15px; border-radius: 6px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">

<img src="/images/portfolio/videoanalysis2.png" alt="Video Analysis Frame 2" style="width: 100%; margin-bottom: 15px; border-radius: 6px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">

<img src="/images/portfolio/videoanalysis3.png" alt="Video Analysis Frame 3" style="width: 100%; margin-bottom: 15px; border-radius: 6px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">

<img src="/images/portfolio/videoanalysis4.png" alt="Video Analysis Frame 4" style="width: 100%; margin-bottom: 15px; border-radius: 6px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">

<img src="/images/portfolio/videoanalysis5.png" alt="Video Analysis Frame 5" style="width: 100%; margin-bottom: 15px; border-radius: 6px; box-shadow: 0 2px 4px rgba(0,0,0,0.1);">

  </div>
</details>

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

<h3 style="margin-top: 40px;">Race Metrics</h3>
<p>Select a race from the map to view the physiological metrics recorded sequentially over the course of the run, mapping how changes in elevation interact with heart rate.</p>

<div style="display: flex; gap: 10px; margin-bottom: 20px;">
  <button onclick="loadChart('/assets/data/Servus_Credit_Union_Marathon_metrics.json', 'Marathon')" style="padding: 8px 16px; cursor: pointer; border: 0px solid #ccc; border-radius: 4px; background: #e74c3c; color: white; font-weight: bold; flex: 1;">Marathon</button>
  <button onclick="loadChart('/assets/data/Last_Chance_Half_Marathon_metrics.json', 'Half-Marathon')" style="padding: 8px 16px; cursor: pointer; border: 0px solid #ccc; border-radius: 4px; background: #27ae60; color: white; font-weight: bold; flex: 1;">Half-Marathon</button>
  <button onclick="loadChart('/assets/data/Dino_Dash_5k__metrics.json', '5K')" style="padding: 8px 16px; cursor: pointer; border: 0px solid #ccc; border-radius: 4px; background: #2980b9; color: white; font-weight: bold; flex: 1;">5K</button>
</div>

<div style="width: 100%; border: 1px solid #ddd; padding: 15px; border-radius: 8px; box-sizing: border-box;"><canvas id="raceChart" height="120"></canvas></div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
  let raceChart;

  function loadChart(url, title) {
    fetch(url).then(res => res.json()).then(data => {
      const ctx = document.getElementById('raceChart').getContext('2d');
      
      if (raceChart) {
          raceChart.destroy();
      }
      
      raceChart = new Chart(ctx, {
          type: 'line',
          data: {
              labels: data.distance,
              datasets: [
                  {
                      label: 'Heart Rate (bpm)',
                      data: data.heart_rate,
                      borderColor: 'rgba(231, 76, 60, 1)',
                      backgroundColor: 'rgba(231, 76, 60, 0.1)',
                      yAxisID: 'y',
                      fill: true,
                      tension: 0.4,
                      pointRadius: 0,
                      borderWidth: 2
                  },
                  {
                      label: 'Elevation (m)',
                      data: data.altitude,
                      borderColor: 'rgba(41, 128, 185, 1)',
                      backgroundColor: 'rgba(52, 152, 219, 0.1)',
                      yAxisID: 'y1',
                      fill: true,
                      tension: 0.4,
                      pointRadius: 0,
                      borderWidth: 2
                  },
                  {
                      label: 'Pace (min/km)',
                      data: data.pace,
                      borderColor: 'rgba(155, 89, 182, 1)',
                      backgroundColor: 'rgba(155, 89, 182, 0.1)',
                      yAxisID: 'y2',
                      fill: false,
                      tension: 0.4,
                      pointRadius: 0,
                      borderWidth: 2,
                      borderDash: [5, 5]
                  }
              ]
          },
          options: {
              responsive: true,
              interaction: {
                  mode: 'index',
                  intersect: false,
              },
              plugins: {
                  title: {
                      display: true,
                      text: title + ' Physiological Metrics'
                  }
              },
              scales: {
                  x: {
                      title: { display: true, text: 'Distance (km)' }
                  },
                  y: {
                      type: 'linear',
                      display: true,
                      position: 'left',
                      title: { display: true, text: 'Heart Rate (bpm)' }
                  },
                  y1: {
                      type: 'linear',
                      display: true,
                      position: 'right',
                      title: { display: true, text: 'Elevation (m)' },
                      grid: { drawOnChartArea: false }
                  },
                  y2: {
                      type: 'linear',
                      display: true,
                      position: 'right',
                      title: { display: true, text: 'Pace (min/km)' },
                      grid: { drawOnChartArea: false },
                      reverse: true
                  }
              }
          }
      });
    }).catch(err => console.error("Error loading chart data: ", err));
  }

  // Load Marathon by default
  document.addEventListener("DOMContentLoaded", function() {
      loadChart('/assets/data/Servus_Credit_Union_Marathon_metrics.json', 'Marathon');
  });
</script>
