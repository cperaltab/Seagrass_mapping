Output/product: seagrass map for Belize > Placencia area and out to reef also, and for Caye Caulker area (Maya Trotz -CoPe).

Time frame: search for imgages'2024-11-01', '2025-06-30' 


_Workflow_
**Image selection:** Filtering the image collection to get best quality of images to use for the classification. In GEE filter the Sentinel-2 L2A Harmonized image collection '2024-11-01', '2025-06-30' = to 1017 images for the AOI and time frame selected; export the CSV of the image collection with properties and select manually the images from the Tiles of interest and Cloud Pixel percentage <20%. When applying an automated nos-supervised cloud cover filter we get 779 cloud fileterd, cloud masked images (see GEE scripts). When applyin an automated, non supervised filter and cloud mask **for the specific tiles** I get 0 images (!).



Tiles of interest: T16QCD and T16QCE

|ImageID|imageDate|Number of images|
|:-----:|:-------:|:--------------:|
|T16QCD|2025-03| 2 |
|T16QCE|2025-03| 2 |
|T16QCE|2025-04| 1 |
|T16QCE|2025-06| 1 |

After manualy filtering by tiles, a total of 173 images filtered from the S-2A SR (https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR_HARMONIZED) for 2025, with <20% cloud cover filtered manually from the CSV file exported. 6 selected images manualy with less than 20% cloud pixel percentage. 



**Image pre-processing (selection of the image):** we will work on individual Tiles, perfomr the classification pero individual images and then calculate the median to get the final seagrass cover polygon (see My Handbook and Luis notes). After performing classification per image we need to export the classified image as an assetn the create the final mosaic for the classification.

Normalized Difference Water Index (NDWI) is calculated using the following formula: (Green - NIR) / (Green + NIR) Water bodies typically have higher reflectance in the green band and lower reflectance in the NIR band; calculation results in values ranging from -1 to +1. Water bodies usually have positive NDWI values, while vegetation and built-up areas tend to have lower or negative values. 

**Groundtruth database creation:** data points taken from Claudia's visit to Belize (2024), GPS data recording and bothom type identification. Additional seagrass data points from SegrassNet site. No seagrass occurrence data in OBIS. Scleractinia data points taken from OBIS. Imported all data points (104 in total) to GoogleEarth Pro and check accuracy of points and benthic habitat verification; used seagrass, sand and hardbottom type (including Scleractinia). Scleractinia data are very poor and not enough for a significant class but could help to perform a better image interpretation when selecting points for class training de chosed model. 

Use Allen Coral Atlas Geomorphic Zone map and the Benthic Habitat Map for guidance in creating the class points for training the model. The raster and vector layers for this map is in my QGIS project. Note: no benthic habitat classes for the continetal area of Belize, only for the islands and off-shore areas.
Upload the geomorphic zone and benthic habitat map to GEE as an asset (250GB space per GEE Cloud Project; I had to work on another project because the imars-simm has no more space).
Use the Allen Coral Atlas bathymetry raster to frame the depth of the study area: how deep are we performing the seagrass detection/mapping? How to tell the machine learning algorithm to perform the classification up to 10mt depth

Geomorphic zone map: helps identify biological/ecological areas> reef areas, coastal lagoons, sandy areas, etc. Land shallow ocean mask with geomorphic zone map for creating this mask.
Bathynetry map (up to 12m depth)
Classification map using the previous masks. "Parental guidance in classifying: 1) Geomorphic zones map as a guide 2) Seeding process where you feed the information on the geomorphic zone to refine the classification
see Caribbean Benthic Mapping webinar: https://reefresilience.org/caribbean-benthic-mapping/
....

**To-do:**

- [x] Filter useful images for Nov-Dec2024 and 2025, for all applicable Tiles (cloud_pixel_percentage); review the ROI polygon befor filtering and visualizing the images. Tiles of interest: 16QCE, 16QCD
- [x] Use Geomorphic and benthic habitat maps for Mesoamerica as a guide (downloaded from the AllenCoral Atlas and upload as asset into my GEE Project)
- [ ] Upload Belize seagrass grountruth data points (Claudia) to GEE and use as training points.
- [ ] After selected images: check and edit all the geometry imports from the previous classification: seagrass vs no seagrass class; **sand_poly**. Use Geomorphic and Habitat maps as a guide to place the points/polygons for grountruthing/training. We can do this per image or per imageCollection
- [x] Look for the batimetry map for all the Caribbean (10mt resolution): 10-12mt depthgood precission; beyond that depth the accuracy is not good. Useful to map benthic habitat up to 12mt depth

Compare output with Allen Coral Atlas or other world benthic habitat mapping 
  








