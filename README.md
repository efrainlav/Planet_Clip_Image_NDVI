## Clip GeoTIFF Image to Bounding Polygon
This script allows you to clip a GeoTIFF image using a specified bounding polygon defined in a GeoJSON file. It also calculates the Normalized Difference Vegetation Index (NDVI) within the polygon region.


### Requirements

- Python 3.x
- `argparse`, `rasterio`, and `numpy` libraries

### Usage

1. Ensure you have Python 3.x installed on your system.
2. Install the required libraries by running the following command:

```shell
pip install argparse rasterio numpy
```

3. Prepare your GeoTIFF image file and GeoJSON bounds file.
4. Open a terminal or command prompt and navigate to the directory containing the script.
5. Run the script with the following command:

```shell
python clip_image.py --image T11SLU_20200925T183121_4Band_clip.tif --bounds bounds.geojson --output result.tif
```


### Code explanation

The script performs the following steps:

1. Imports the necessary libraries (`argparse`, `rasterio`, `json`, and `numpy`).
2. Defines a function `clip_image_to_polygon` that takes the image path, bounds path, output path, and an optional projection parameter.
3. The function initializes the `polygon_mask` variable.
4. Opens the image file using `rasterio.open` and reads the GeoJSON file using `open` and `json.load`.
5. Extracts the geometry from the GeoJSON file.
6. Clips the image to the polygon using `rasterio.mask` and obtains the clipped image and its transform.
7. Creates a boolean mask indicating pixels inside the polygon.
8. Calculates the NDVI using the red and NIR bands of the clipped image (Assuming that the input image has 4 bands, with band 3 being Red and band 4
being NIR).
9. Applies the mask to the NDVI to assign non-zero values to areas outside the polygon.
10. Updates the metadata for the clipped image, including height, width, transform, CRS, driver, and data type.
11. Writes the clipped image to a new file using `rasterio.open` and `write`.
12. Updates the metadata for the NDVI image, specifying the number of bands and data type.
13. Saves the NDVI as a separate image using `rasterio.open` and `write`.
14. If an exception occurs, it prints an error message.
15. If the script is executed directly (not imported), it parses the command-line arguments using `argparse.ArgumentParser`.
16. Calls the `clip_image_to_polygon` function with the provided command-line arguments.

<div style="display: flex;">
  <div style="flex-basis: 40%;">
    <figure>
      <img src="image/img1.JPG" alt="Image 1" style="width: 50%;">
      <figcaption>Figure 1. The original image.</figcaption>
    </figure>
  </div>
  <div style="flex-basis: 30%;">
    <figure>
      <img src="image/img2.png" alt="Image 2" style="width: 30%;">
      <figcaption>Figure 2. Clip image.</figcaption>
    </figure>
  </div>
  <div style="flex-basis: 30%;">
    <figure>
      <img src="image/img3.png" alt="Image 3" style="width: 30%;">
      <figcaption>Figure 3. NDVI - Clip image.</figcaption>
    </figure>
  </div>
</div>  
