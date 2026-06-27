# aerial-triangulation-lps-erdas
Aerial Triangulation, DTM Generation &amp; Digital Orthophoto Production
# 📍 Aerial Triangulation, DTM Generation & Digital Orthophoto Production
### Using ERDAS IMAGINE 2013 — Leica Photogrammetry Suite (LPS)

## Overview

This repository documents a complete photogrammetric workflow applied to aerial imagery of **Addis Ababa, Ethiopia (2002)**. The workflow covers everything from block file creation to the final mosaicked orthophoto, carried out using **ERDAS IMAGINE 2013 / Leica Photogrammetry Suite (LPS)**.

The study area is processed using one strip of three overlapping aerial photographs, a calibrated frame camera, and six full ground control points (GCPs), resulting in a georeferenced Digital Terrain Model (DTM) and Digital Orthophoto.

---

## Dataset

| Item | Details |
|---|---|
| Imagery | Aerial photos of Addis Ababa, 2002 |
| Format | Scanned dia-positive, converted to `.tif` / `.img` |
| Strip | 1 strip — 3 images with 60% forward overlap |
| Image IDs | `4094`, `4093`, `4092` |
| Camera | RMK Top15 (Frame Camera) |
| Focal Length | 153.2550 mm |
| Principal Point xo | 0.0100 mm |
| Principal Point yo | −0.0060 mm |
| Number of Fiducials | 8 |
| GCPs | 6 full ground control points |
| Projection | UTM Zone 37 North |
| Spheroid | Clarke 1880 |
| Datum | Adindan (Ethiopia) |
| Elevation Units | Meters |
| Software | ERDAS IMAGINE 2013 / LPS |

---

## Ground Control Points

| GCP # | X (m) | Y (m) | Z (m) |
|---|---|---|---|
| 1 | 483404.75 | 995082.83 | 2363.62 |
| 2 | 483383.47 | 993892.89 | 2314.72 |
| 3 | 483868.54 | 994987.83 | 2362.16 |
| 4 | 484081.12 | 994171.90 | 2345.36 |
| 5 | 484471.67 | 995060.63 | 2344.16 |
| 6 | 484608.17 | 994037.14 | 2318.96 |

---

## Perspective Center Coordinates (Approximate)

| Strip | Image | Xo (m) | Yo (m) | Zo (m) |
|---|---|---|---|---|
| 1 | 4094 | 483454.982 | 994479.632 | 3332.899 |
| 1 | 4093 | 484007.317 | 994482.468 | 3338.793 |
| 1 | 4092 | 484560.703 | 994485.851 | 3341.008 |

---

## Workflow

### Step 1 — Create a New Project

1. Launch **ERDAS IMAGINE 2013** and open **Leica Photogrammetry Suite (LPS)**
2. Create a working directory: `D:/dig-photo`
3. Go to **File > New** and create a new block project file: `Bole_Block.blk`

---

### Step 2 — Model Setup

1. From **Model Setup**, select **Geometric Model Category: Camera**
2. Set **Geometric Model: Frame Camera**
3. In **Block Property**, set the horizontal projection:
   - Standard: UTM WGS 84
   - Projection Type: UTM
   - Spheroid: Clarke 1880
   - Datum: Adindan (Ethiopia)
   - UTM Zone: 37 North
4. Set the vertical projection:
   - Spheroid: Clarke 1880
   - Datum: Adindan (Ethiopia)
   - Elevation Units: Meters
   - Elevation Type: Height
5. Click **Next** and set **Average Flying Height: 912 meters**

---

### Step 3 — Add Images to the Block

1. Go to **Edit > Add Frame**
2. Navigate to your image folder and set file type to `.img` / `.tif`
3. Select all three images (`4094`, `4093`, `4092`) and click **OK**
4. When pyramid generation completes, both Pyramid and Online columns turn **Green**

---

### Step 4 — Define the Camera (Sensor)

1. Go to **Edit > Frame Editor**, click on **Sensor > Camera**
2. Enter the following under the **General** tab:

   | Parameter | Value |
   |---|---|
   | Camera Name | RMK Top15 |
   | Description | Frame camera |
   | Focal Length | 153.2550 mm |
   | Principal Point xo | 0.0100 mm |
   | Principal Point yo | −0.0060 mm |

3. Under the **Fiducials** tab, enter all 8 fiducial coordinates
4. Under **Radial Lens Distortion**, enter distortion values
5. Click **OK**

---

### Step 5 — Interior Orientation

1. In **Frame Camera Frame Editor**, go to the **Interior Orientation** tab
2. Set the photo orientation to **180°** (flight direction) using the rotation icon
3. Click the transfer icon and mark the center of each fiducial on the image
4. Click **Next** to repeat for the remaining photos
5. When complete, the **Int.** column turns **Green** (RMSE should be ≤ 0.5 pixels)

---

### Step 6 — Exterior Orientation

1. In **Frame Camera Frame Editor**, go to the **Exterior Information** tab
2. Enter the perspective center coordinates (Xo, Yo, Zo) for each image:

   | Image | Xo | Yo | Zo | Kappa |
   |---|---|---|---|---|
   | 4094 | 483454.982 | 994479.632 | 3332.899 | 180° |
   | 4093 | 484007.317 | 994482.468 | 3338.793 | 180° |
   | 4092 | 484560.703 | 994485.851 | 3341.008 | 180° |

3. Click **Next** or use **Edit All Images** to enter values for all at once
4. When complete, image footprints of the strip appear on the map view

---

### Step 7 — Import ASCII Ground Control Points

1. Go to **Edit > Point Measurement**
2. Select **Classical Point Measurement Tool** and click **OK**
3. Click **Add** to insert 6 GCP rows
4. Hold **Shift** and select the X, Y, Z reference columns
5. Right-click the X Reference column header and select **Import**
6. Select `gcp.txt` from your folder
7. Click **Option** and set **Separation Character: White Space**
8. Click **OK**
9. Change column **Type** to `Full` and **Usage** to `Control`

---

### Step 8 — Measure Control Points on Images

1. Display Image `4094` in the Left View and `4093` in the Right View
2. Using the crosshair tool (+), locate and mark the exact position of each GCP on both images
3. Repeat for all 6 GCPs across all overlapping image pairs
4. Save measurements when complete

**GCP Photo Locations:**

| GCP | Image | Location Description |
|---|---|---|
| TP-1 | 4094 | Corner of small house |
| TP-2 | 4094 | Corner of parcel boundary |
| TP-3 | 4093 | Corner of basement |
| TP-4 | 4093 | Corner of wooden fence |
| TP-5 | 4092 | Corner of parcel boundary |
| TP-6 | 4092 | Corner of parcel boundary |

---

### Step 9 — Automatic Tie Point Generation

1. Click the **Automatic Tie Point Generation** icon
2. In the **General** tab:
   - Images Used: All Available
   - Initial Type: Tie Points
   - Image Layer: 1
   - Existing Point Transfer: No Transfer, New Points Only
3. In the **Strategy** tab:
   - Search Size: 21
   - Correlation Size: 7
   - Least Square Size: 21
   - Feature Point Density: 100%
   - Coefficient Limit: 0.80
   - Initial Accuracy: 10%
4. In the **Distribution** tab:
   - Intended Number of Points/Image: 60
5. Click **Run** and wait for completion
6. Review generated tie points and remove any with large residuals

---

### Step 10 — Aerial Triangulation

1. Click the **Aerial Triangulation** icon (triangle)
2. Set **Type: Same Weighted Value** and leave all other settings at default
3. Click **Run**
4. Review the **Triangulation Report** for residuals
5. Analyze and refine until acceptable accuracy is achieved

**Triangulation Summary Results:**

| Metric | Value |
|---|---|
| Convergence | Yes |
| Total Image Unit-Weight RMSE | 0.1996 |
| Control Point RMSE — Ground X | 0.1764 m |
| Control Point RMSE — Ground Y | 0.1834 m |
| Control Point RMSE — Ground Z | 0.8595 m |
| Control Point RMSE — Image X | 0.0452 px |
| Control Point RMSE — Image Y | 0.4501 px |

---

### Step 11 — DTM Generation

1. Go to **Process > DTM Extraction**
2. Set **Output DTM Type: Terramodel TIN**
3. Set **Output Form: Single DTM Mosaic**
4. Set DTM Cell Size: 10 m × 10 m
5. Specify output path: `terrain_dtm.pro`
6. Click **Run**
7. When complete, the **DTM** column turns **Green**

---

### Step 12 — Orthophoto Generation

1. Go to **Process > Ortho Rectification > Resampling**
2. In the **General** tab:
   - DTM Source: Terramodel TIN
   - TIN File: `terrain_dtm.pro`
3. Click **Add** and select all three images
4. Assign output names: `ortho_n4094.img`, `ortho_n4093.img`, `ortho_n4092.img`
5. In the **Advanced** tab:
   - Resampling Method: **Nearest Neighbor**
   - Overlap Threshold: 50%
6. Click **OK** and run for all images

---

### Step 13 — Subsetting (Cropping Active Areas)

1. Display each orthophoto in the Viewer
2. Go to **AOI > Tools** and draw a rectangle over the active area only
3. Go to **Data Preparation > Subset Image**
4. Specify Input/Output file names
5. Click **AOI** and select **Viewer** to use your drawn AOI
6. Repeat for all three orthophotos

---

### Step 14 — Mosaic

1. Go to **Data Preparation > Mosaic Images > Mosaic Tool**  
   or **Process > Mosaic > Mosaic Tool**
2. Click the **Add Images** button and load all subsetted orthophotos
3. Go to **Edit > Set Overlap Function > Feather** — click **Apply**, then **Close**
4. Go to **Edit > Color Correction > Use Image Dodging** — click **OK**
5. Go to **Process > Run Mosaic**
6. Display the final mosaic (`new_mos.img`) in a new Viewer

---

## Outputs

| Output | Description |
|---|---|
| `terrain_dtm.pro` | Digital Terrain Model — Terramodel TIN format |
| `ortho_n4094.img` | Rectified orthophoto — image 4094 |
| `ortho_n4093.img` | Rectified orthophoto — image 4093 |
| `ortho_n4092.img` | Rectified orthophoto — image 4092 |
| `new_mos.img` | Final mosaicked orthophoto of the full strip |

---

## Tools & Software

- **ERDAS IMAGINE 2013**
- **Leica Photogrammetry Suite (LPS)**
- Camera: RMK Top15 (Frame Camera)
- Projection: UTM Zone 37N, Clarke 1880 / Adindan (Ethiopia)

---

## Author

**Abel Tesfaye**  
Assistant Lecturer — Bahir Dar University  
GIS | Remote Sensing | UAV | Photogrammetry  
🔗 [github.com/abel-tesfaye-geo](https://github.com/abel-tesfaye-geo)
