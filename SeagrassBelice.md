**3) Seagrass map for Belize**

GEE project: https://code.earthengine.google.com/0f8f76e5e20e18eb057bcc0328408b10 

_Workflow_

1.- Groundtruth database creation: data points taken from Claudias visit to Belize, GPS data recording and bothom type identification. Seagrass data points from SegrassNet site. No seagrass occurrence data in OBIS. Scleractinia data points taken from OBIS. 
Imported all data points (104 in total) to GoogleEarth Pro and check accuracy of points and benthic habitat verification; used seagrass, sand and hardbottom type (including Scleractinia). Scleractinia data are very poor and not enough for a significant class.

Looking for different satellite images dates in Google Earth Pro to get the better image (no clouds, no turbidity, good resolution); some points were on top of mangroves, some other points were hard to confirm the type of habitat it was representing. No celar view of the bottom. Market in green the verified points which will be used after for the training points (featureCollection in GEE).
The data points available are from Bacalar Chico down to Punta Gorda (inland)

2.- Image selection: region of interest, time frame of the collection.

For a baseline map select the best image possible (with less cloud cover possible)
Tiles for Belice coastal area using Sentinel 2 image collection are: 16QCE, 16QDE, 16QCD, 16QDD, 16PCC. For the baseline map and according to the specific AOI for the CoPe project we worked only with 16QCD tile. You can see the specific tile codies here: https://eatlas.org.au/geonetwork/srv/eng/catalog.search#/metadata/f7468d15-12be-4e3f-a246-b2882a324f59 

For the baseline map I selected one single image per year/tile (2020-2022):

idB2 = '20210411T160901_20210411T162810_T16QCD' // image with 1%< Cloud pixels

After trying with more recent images we got that for 2022 and 2023 we have we have cero images for our tile (T16QCD), with 1%< Cloud pixels. 1.83% cloud coverage we found only one image for 2023 and one with 3.64% cloudy pixels.

...

No good images for 2023-2024> no images for the specific tile, fractions of an image, to much clouds.



![image](https://github.com/cperaltab/Seagrass_mapping/assets/7772503/c5302163-2ac2-44ec-8d09-886c76841922)

3. Pre-processing: for baseline map we used the best image (single image). Applied Masks: cloud; missing water, land and glint mask.
   Create FetaureCollection for training data points using the groundtruth data.
   Create sand polygons (FeatureCollection) for Depth Invariant Index.. see notes to elaborate on this.

4. Classification: select the bands to sample "sampling bands"==> B1, B2, B3, B4, B2B3
   Sample bands with ground-truth dataset (70% training, 30% validation)
   Train SVM (Support Vector Machine) model and classify. The SVM is a machine-learning approach for supervised classification and 
   regression. Mode of operation is per pixel/per feature.
   Get accuracies and Kappa coefficients. At this moment my Kappa is low: 0.587; accuracy for softbottom = 1; hardbottom = 0.18; seagrass 
   = 0.76. Issue: not enough hardbottom data points (ground truth); try the classification with only softbottom (sand) and seagrass data 
   points.

5. Post-Classification: classified image; select pixels classified as seagrass; map edition and post-classification; final product.

   Export the final image as GeoTiff to GoogleDrive. Download the tif file to the local computer. Add raster layer into QGIS. Add background map. Add grid, coordinates and labels. Export as PNG or JPEG.

    See QGIS tutorial for adding raster layer: https://usfedu-my.sharepoint.com/personal/bryant117_usf_edu/_layouts/15/stream.aspx?id=%2Fpersonal%2Fbryant117%5Fusf%5Fedu%2FDocuments%2FRecordings%2FQGIS%20Walk%20through%2D20240614%5F175229%2DMeeting%20Recording%2Emp4&ct=1718499603348&or=Teams%2DHL&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2Eb02ae252%2D58b7%2D494a%2Dbc7b%2De6277584ab29 

_Caviats_

* Check the Kappa and Accuracy values. Not good
* Check the training points and number of classes. More grountruth needed for every class
* Check the Depth Invariant Index. 
* Check Water and land masks.
* Correct the seagrass overestimation and seaagrass class inland, up into the rivers.




