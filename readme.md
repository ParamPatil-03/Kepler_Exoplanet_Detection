# Exoplanet Detection using Lightkurve: Kepler-90 Case Study

This repository contains a Jupyter Notebook that demonstrates how to analyze stellar light curve data to detect the presence of exoplanets using the transit method. The analysis focuses on **Kepler-90**, a star famous for hosting a multi-planetary system similar in scale to our own Solar System.

---

## 🚀 Overview

The workflow processes raw brightness data from the Kepler Space Telescope to identify periodic dips in light caused by a planet transiting (passing in front of) the host star. 

By utilizing a **Box Least Squares (BLS)** periodogram, the script attempts to find the orbital period of the detected exoplanet candidate and evaluates the results against confirmed NASA exoplanet archive data.

---

## 🛠️ Method & Code Structure

The analysis is broken down into the following key steps:

### 1. Data Retrieval and Stitching
Queries the Mikulski Archive for Space Telescopes (MAST) using `lightkurve` to find and download all available light curves for Kepler-90 recorded by the Kepler mission, stitching them into a single continuous time-series dataset.

### 2. Light Curve Cleaning
To isolate potential transit signals from stellar variability and instrumental noise, the data is preprocessed:
* **Flattening:** A Savitzky-Golay filter (`window_length=401`) is applied to remove long-term trends.
* **Outlier Removal:** High-sigma anomalies ($20\sigma$) and NaNs are purged.

### 3. Periodogram Evaluation (BLS)
A Box Least Squares periodogram searches across a defined linear spacing of trial periods (0.5 to 16 days) to look for the most statistically significant, recurring box-shaped dips.

### 4. Phase Folding
The light curve is phase-folded using the detected "best-fit" orbital period to overlay all individual transits on top of each other, visually confirming the transit signal profile.

---

## 📊 Key Results & Analysis

| Parameter | Value / Finding |
| :--- | :--- |
| **Target Star** | Kepler-90 |
| **BLS Extracted Period** | ~15.789 days |
| **Closest Match (NASA Archive)** | Kepler-90i (~14.448 days) |

### Context & Limitations
While the code successfully identifies a prominent planetary transit signal, the calculated period (~15.79 days) does not perfectly match the officially confirmed period of **Kepler-90i** (14.45 days). 

> **Why the discrepancy?**
> 1. **Multi-Planetary Interference:** Kepler-90 is a crowded system with 8 known planets. The overlapping gravitational signals and transits of neighboring planets introduce transit timing variations (TTVs) and signal interference.
> 2. **Harmonics/Alias Signals:** Simple BLS searches can easily latch onto mathematical harmonics or aliased frequencies of the true orbital period when dealing with dense, multi-transit data.
> 3. **Methodology:** Kepler-90i's discovery in 2017 heavily relied on deep learning and advanced signal-parsing pipelines, proving that a standalone basic BLS method has limitations in complex systems.

---

## 📦 Requirements & Installation

To run this notebook locally, ensure you have Python installed along with the required libraries:

```bash
pip install lightkurve numpy matplotlib