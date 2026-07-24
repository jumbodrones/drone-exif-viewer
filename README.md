# Drone EXIF Viewer

A simple, browser-based tool for inspecting the geographic and camera metadata stored in DJI drone imagery. Drop in a photo and it displays GPS position, altitude, gimbal orientation, and camera settings, then plots the image location and its ground footprint on an interactive map.

Everything runs locally in your web browser — **your images are never uploaded to any server.**

## Using the tool

1. Open the tool in a web browser (Chrome, Firefox, Edge, or Safari).
2. Drag a drone image onto the drop zone, or click **Choose Image** to browse for one.
3. Read the metadata in the left panel and explore the location on the map at right.
4. Click **⟳ Change** (top-left of the preview) to load a different image.

## What you'll see

The left panel groups the metadata into sections:

- **GPS & Position** — latitude/longitude (decimal and DMS), absolute and relative altitude, RTK status.
- **Flight & Gimbal** — aircraft and gimbal pitch/roll/yaw, with compass widgets, plus ground speed.
- **Camera & Lens** — make, model, sensor size, focal length, field of view, aperture, shutter, ISO.
- **Image Info** — capture date/time, pixel dimensions, color space, software.
- **Spectral / Thermal** — appears only for multispectral or thermal files (band, wavelength, emissivity, etc.).
- **Computed Values** — estimated Ground Sample Distance (GSD), footprint dimensions, coverage area, and shot type (nadir/oblique).

On the map you can switch between **Road** and **Satellite** basemaps and toggle the **Location** marker and the image **Footprint** overlay. The airplane marker points in the direction the camera was facing (gimbal yaw), matching the footprint rectangle.

## Supported drones

The tool recognizes most current DJI cameras, including the Mini 3/4/5 Pro, Air 2/2S/3, Mavic 2/3 (incl. Enterprise, Multispectral, and Thermal), Phantom 4, Matrice 30/30T and Matrice 4/4T, and Inspire/Zenmuse cameras. For any model not explicitly listed, it falls back to the 35mm-equivalent focal length in the file, so the footprint and GSD still compute correctly.

Multispectral TIFF bands (Mavic 3M) and thermal files (M30T, M4T) are supported for metadata and mapping. Note that per-pixel temperature extraction from thermal images requires DJI's Thermal SDK and is not available in a browser.

## Requirements and notes

- **Internet connection required.** The map and metadata libraries load from the web, and map tiles stream on demand.
- **A footprint needs three things** in the image: GPS coordinates, altitude, and a focal-length tag. If one is missing, the Computed Values panel names which. Images that have been re-exported or stripped of metadata may not have all three.
- **TIFF and DNG files** parse fully, but browsers can't display them as a preview image — you'll see a placeholder while the metadata and map still work normally.

---

*Client-side tool — no data leaves your computer. Built for coursework in drone data capture and analysis.*

