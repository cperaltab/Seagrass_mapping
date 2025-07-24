Output/product: seagrass map for Belize > Placencia area and out to reef also, and for Caye Caulker area (Maya Trotz -CoPe).

Time frame: 2025???


_Workflow_

**1.- Groundtruth database creation:** data points taken from Claudia's visit to Belize (2024), GPS data recording and bothom type identification. Additional seagrass data points from SegrassNet site. No seagrass occurrence data in OBIS. Scleractinia data points taken from OBIS. Imported all data points (104 in total) to GoogleEarth Pro and check accuracy of points and benthic habitat verification; used seagrass, sand and hardbottom type (including Scleractinia). Scleractinia data are very poor and not enough for a significant class but could help to perform a better image interpretation when selecting points for class training de chosed model. 

Geomorphic zone map: helps identify biological/ecological areas> reef areas, coastal lagoons, sandy areas, etc. Land shallow ocean mask with geomorphic zone map for creating this mask.
Bathynetry map (up to 12m depth)
Classification map using the previous masks. "Parental guidance in classifying: 1) Geomorphic zones map as a guide 2) Seeding process where you feed the information on the geomorphic zone to refine the classification
see Caribbean Benthic Mapping webinar: https://reefresilience.org/caribbean-benthic-mapping/
....

**To-do:**

- Filter useful images for Nov-Dec2024 and 2025, for all applicable Tiles (cloud_pixel_percentage); review the ROI polygon befor filtering and visualizing the images. Tiles of interest: 16QCE, 16QCD
- After selected images: check and edit the geometry imports: seagrass vs no seagrass class; sand_poly. Use Geomorphic and benthic habitat maps for Mesoamerica as a guide (downloaded from the AllenCoral Atlas)

(*) Look for the batimetry map for all the Caribbean (10mt resolution): 10-12mt depthgood precission; beyond that depth the accuracy is not good. Useful to map benthic habitat up to 12mt depth
Compare output with Allen Coral Atlas or other world benthic habitat mapping 




