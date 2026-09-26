# Drone EXIF Viewer

A simple, browser-based tool for inspecting the geographic and camera metadata stored in DJI drone imagery. Drop in a photo and it displays GPS position, altitude, gimbal orientation, and camera settings, then plots the image location and its ground footprint on an interactive map.

Everything runs locally in your web browser — **your images are never uploaded to any server.**

## Using the tool

1. Open the tool in a web browser (Chrome, Firefox, Edge, or Safari).
2. Drag one or more drone images onto the drop zone, or click **Choose Images** to browse.
3. Read the metadata in the left panel and explore the locations on the map at right.
4. When several images are loaded, a **thumbnail strip** appears at the top of the left panel — click any thumbnail (or any marker/footprint on the map) to see that image's full metadata.

### Measuring distances

Click **📏 Measure** in the map toolbar to open the selected image at full size, then click two points on the photo. The tool reports the distance in the image's full-resolution **pixels** and, using the estimated GSD, the corresponding **ground distance** in meters. Use **+ / − / Fit** or the **mouse wheel** to zoom in for precise point placement — measurements stay accurate at any zoom level — and **right-click and drag to pan** around a zoomed image. A third click starts a new measurement; **Reset** clears it and **Close** (or Esc) exits. Ground distance is most accurate for near-nadir imagery over flat terrain. (Available for JPEG/PNG; TIFF and DNG can't be displayed for measuring.)

### Loading a whole flight

You can load an entire mission at once. Every image's location and ground footprint plots on the map together, so you can see survey coverage and overlap at a glance. The selected image is highlighted; the rest are shown as dots and faint footprint outlines.

**Click any thumbnail to show or hide that image on the map** — its marker, footprint, and draped photo appear or disappear, and the thumbnail dims when hidden. This lets you isolate individual images or build up a coverage view a few at a time. Use **👁 All** / **🚫 None** to show or hide everything at once. (Clicking a thumbnail also loads that image's metadata into the panel, so you can still read its details either way.)

Use **+ Add** to add more images to the batch, **⬇ CSV** to download a spreadsheet of all loaded images' metadata (filename, GPS, altitude, model, GSD, footprint size, band, etc.), and **Clear** to start over.

## What you'll see

The left panel groups the metadata into sections:

- **GPS & Position** — latitude/longitude (decimal and DMS), absolute and relative altitude, RTK status.
- **Flight & Gimbal** — aircraft and gimbal pitch/roll/yaw, with compass widgets, plus ground speed.
- **Camera & Lens** — make, model, sensor size, focal length, field of view, aperture, shutter, ISO.
- **Image Info** — capture date/time, pixel dimensions, color space, software.
- **Spectral / Thermal** — appears only for multispectral or thermal files (band, wavelength, emissivity, etc.).
- **Computed Values** — estimated Ground Sample Distance (GSD), footprint dimensions, coverage area, and shot type (nadir/oblique).

On the map you can switch between **Road** and **Satellite** basemaps and toggle three layers: the **Location** markers, the image **Footprint** outlines, and **Drape images** — which places each photo inside its own footprint on the map, forming a rough live orthomosaic of the flight. (Draping works for JPEG/PNG images; TIFF and DNG can't be drawn by the browser, so those show their footprint outline only.) The airplane marker points in the direction the camera was facing (gimbal yaw), matching the footprint rectangle.

## Supported drones

The tool recognizes most current DJI cameras, including the Mini 3/4/5 Pro, Air 2/2S/3, Mavic 2/3 (incl. Enterprise, Multispectral, and Thermal), Phantom 4, Matrice 30/30T and Matrice 4/4T, and Inspire/Zenmuse cameras. For any model not explicitly listed, it falls back to the 35mm-equivalent focal length in the file, so the footprint and GSD still compute correctly.

Multispectral TIFF bands (Mavic 3M) and thermal files (M30T, M4T) are supported for metadata and mapping. Note that per-pixel temperature extraction from thermal images requires DJI's Thermal SDK and is not available in a browser.

## Requirements and notes

- **Internet connection required.** The map and metadata libraries load from the web, and map tiles stream on demand.
- **A footprint needs three things** in the image: GPS coordinates, altitude, and a focal-length tag. If one is missing, the Computed Values panel names which. Images that have been re-exported or stripped of metadata may not have all three.
- **TIFF and DNG files** parse fully, but browsers can't display them as a preview image — you'll see a placeholder while the metadata and map still work normally.

---

*Client-side tool — no data leaves your computer. Built for coursework in drone data capture and analysis.*
