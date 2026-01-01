# Development of a DGNSS Tool for Android Smartphones using Raw Measurements

![Status](https://img.shields.io/badge/Status-Proprietary%20%2F%20R%26D-blueviolet)
![Support](https://img.shields.io/badge/Supported%20By-TÜBİTAK%202209--A-blue)
![Domain](https://img.shields.io/badge/Domain-Geomatics%20%7C%20Navigation-orange)

> ** This repository showcases the R&D work for a TÜBİTAK 2209-A supported 2024-2025 academic year graduation project. Due to the proprietary nature of the developed algorithms, the source code is closed. This document outlines the project scope, architectural design, and methodology.

## Abstract
Raw GNSS data availability in Android (since 2016) unlocked new possibilities for low-cost positioning. However, smartphone GNSS chipsets suffer from high noise and multipath effects, limiting their standalone performance.

This project aims to bridge the gap between low-cost hardware and high-precision requirements. We designed a tool to process Android Raw GNSS observations enhanced with DGNSS (Differential GNSS) corrections obtained from the TUSAGA-Aktif (Turkey National Fixed GNSS Network) CORS network.

The resulting tool targets critical sectors including:
* **Cartography & GIS**
* **Precision Agriculture**
* **Autonomous Navigation**

---

## Proposed System Architecture

The project moves beyond standard SPP by integrating network corrections. The conceptual design involves processing the raw carrier phase and code observations against a reference stream.

```mermaid
graph TD
    subgraph Mobile Segment
    A[Android Smartphone] -->|Raw GNSS Data| B(Data Parsing & Noise Reduction)
    end
    
    subgraph Network Segment
    C[TUSAGA-Aktif Network] -->|RTCM Corrections| D(Correction Decoder)
    end
    
    B --> E{Positioning Engine}
    D --> E
    
    E -->|Apply DGNSS/RTK Logic| F[Atmospheric & Clock Correction]
    F -->|Least Squares Estimation| G[Enhanced Coordinate Output]
