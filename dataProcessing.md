**1) Seagrass map for Venezuela**

Ground truth: a database with all seagrass data points was created; the data points were extrated from the literature. In addition, an old database created for the whole Caribbeanre was re-used. My "raw" database has some columns with information that goes beyond ground truthing. Is for a more ecological assessment. That data will be re-considered later on.
The data points from the raw database has been filtered and the column names has been re-organized to fit for purpose. 

New habitat type records need to be added, e. g. sand, corals, etc.

Data from OBIS and from a seagrass mapping article for Los Roques Island need to be added.

Data from Colombia and Belize needs to be added.

**2) Seagrass map for USVI**

Collaborative work with Edwin Cruz-Rivera (institute???)

May be part of Chealsea's master thesis

Currently in the exploration stage; now reviewing GEE codes and exploring Sentinel 2 images. Need to explore different time ranges beacuse there are to much clouds in the output images.

**3) Seagrass map for Belize**

_Workflow_

1.- Groundtruth database creation: data points taken from Claudias visit to Belize, GPS data recording and bothom type identification. Seagrass data points from SegrassNet site. No seagrass occurrence data in OBIS. Scleractinia data points taken from OBIS. 
Imported all data points (104 in total) to GoogleEarth Pro and check accuracy of points and benthic habitat verification (only used seagrass, sand and hardbottom type), no Scleractinia data were used in the firts clasification run. 

Looking for different satellite images dates in Google Earth Pro to get the better image (no clouds, no turbidity, good resolution); some points were on top of mangroves, some other points were hard to confirm the type of habitat it was representing. No celar view of the bottom. Market in green the verified points which will be used after for the training points (featureCollection in GEE).
The data points available are from Bacalar Chico down to Punta Gorda (inland)

2.- Image selection: region of interest, time frame of the collection.

For a baseline map select the best image possible (with less cloud cover possible)
Tiles for Belice coastal area using Sentinel 2 image collection are: 16QCE, 16QDE, 16QCD, 16QDD, 16PCC. You can see the specific tile codies here: https://eatlas.org.au/geonetwork/srv/eng/catalog.search#/metadata/f7468d15-12be-4e3f-a246-b2882a324f59 

For the baseline map I selected one single image per year/tile (2020-2022):

idB2 = '20210411T160901_20210411T162810_T16QCD' // image with 1%< Cloud pixels
idB3 will try with some more images
idB4
...



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
6. Post-Classification: classified images; select pixels classified as seagrass; create mosaics; map edition and post-classification; final product. This is a missing step and not very critical for a baseline map that uses a single image.






