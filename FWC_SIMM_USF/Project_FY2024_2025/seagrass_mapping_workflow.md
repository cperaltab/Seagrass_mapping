
# ROADMAP

## Phase 1: current seagrass cover for St. Andrew Bay and Ten Thousand Island

# Workflow

**I. Selection of images**

A) **Creating the image collection** 

1. Satellite images will be acquired through the Commercial Small Data Acquisition (CSDA) Program
2. Make the request to NASA for CSDA through IMaRS project
3. Receive the approval and get acces to the different providers imagery (see CSDA-NASA email with instruction)
   
   -For this project we will use Planet: acces and image downloads through Planet account; password provided by CSDA-NASA
   
   -Planet imagery can be accessed through API (limited number of requests)

4. Get images for specific dates/season and AOI
   
   Dates: 2020-2024 
   
   Images downloaded from PlanetExplorer CSDA accounts (Digna and Carolina)
   
   Images archived in USF [Box](https://usf.app.box.com/folder/276967083852)

**_Features for selecting the images from PlanetExplorer_**

Filter to use:
PLANTESCOPE ONLY FILTERS
Spectral bands must include
- Near-infrared (NIR)
- Coastal blue, green I, yellow, red edge
Instrument type
- Super Dove (PSB.SD)
Publishing stage
- Standard
- Finalized

ENVIRONMENTAL CONDITIONS
- Area coverage: (for big areas chose >10%, for smaller areas it can be a higher number)
- Cloud cover: <30% 
- Off-nadir angle: between -30 and 30 degrees (low off-nadir for most mapping applications where minimal distortion is acceptable)
- Sun azimuth: between 135 and 225 degrees (best values for general mapping and vegetation analysis that minimize shadowing while providing even lighting across the scene -->135deg is mid-morning, 225 is mid-afternnon). It can be extended to 100-260 to get more images. 120-230
- Sun elevation: between 45 and 90 degrees (high sun elevation best for minimizing shadows -great for vegetation and  environmental monitoring)

ADVANCED FILTERS
Chose the last one "Show only standard image quality"

If possible, chose images from October to April (low rain and vapor, and no African Dust).

ORDER IMAGERY
Chose Direct Download, GeoTIFF, and press Continue
For the Order Name, include the area and the dates Ex. Rookery_2024_Feb_Mar, press Continue
Only chose "Surface Reflectance - 8 band", press Continue
Chose "Harmonize" and "clip", if present. DO NOT "Composite items", press "Order"

**_Planet Scope product overview:_**

**Instrument:** Planet SuperDove (8-band), third Dove Satellite generation. See more here: https://developers.planet.com/docs/data/planetscope/ 

- 3 m pixel size

- Daily images

- Active since 2020

- 8-Band asset band order (multispectral):


Band 1 = Coastal Blue (431-452 nm)

Band 2 = Blue (465-515 nm)

Band 3 = Green I (513-549 nm)

Band 4 = Green (547-583 nm)

Band 5 = Yellow (600-620 nm)

Band 6 = Red (650-680 nm)

Band 7 = Red Edge (697-713 nm)

Band 8 = Near-infrared (845-885 nm)

Note: the relative spectral response for the SuperDove generation for the Red, Green, Blue, Near Infrared, Red Edge, and Coastal Blue bands closely match those of Sentinel-2A. 

**Products:** 

Item type: PlanetScope [Scene](https://developers.planet.com/docs/data/planetscope/) Planet Platform as PSScene item types.

Asset type: 
|Type                   | Description                                                      |
|-----------------------|------------------------------------------------------------------|
|ortho_analytic_8b_sr	| PlanetScope atmospherically corrected surface reflectance product|
|ortho_analytic_8b_xml  |Radiometrically-calibrated analytic image metadata                |
|ortho_udm2             |Usable data mask (Cloud 2.0). This type strips out any pixels which would not be useful in analysis, including any obscured by haze, shadows, snow or clouds                                    |
   
5. Select the best images to use for classification

-Create a pre-selecton table with all images available: how many images per year or per period of time we have for working on ther classification

File select for [St. Andrew Bay (SAB)](https://usf.box.com/s/wj2uvhrmz4segjth7n71tozg55w0ivx3): 
- 3-4 images per section for 2024
- Images are presented in different scenes (sections) for all the AOI
- Work each image individually and after will create a mosaic for una single image for all the AOI?
Individual remote sensing images can be affected by noisy data, including clouds, cloud shadows, and haze. To produce cleaner images that can be compared more easily across time, we can create ‘summary’ images or ‘composites’ that combine multiple images into one.

A median composite is ideal for creating a reliable, noise-free representation of seagrass habitats. It minimizes the impact of transient factors and produces data consistently enough for accurate classification and change detection.
   
-Top of the atmosphere collection???
   
-Normalized Difference Turbidity Index (NDTI) mean values of valid pixels

 
B) **Creating the ground-truth data points inventory**

Gather all ground-truth data points possible. Search on different sources (Literature, Projects, OBIS, etc.)
See Luis Lizcano-Sandoval database and [FWC geodata portal](https://geodata.myfwc.com/datasets/myfwc::seagrass-habitat-in-florida/about)

II. **Image pre-processing**

1. Do we need to perform Atmospheric correction? The images from Plante Scope have Atmospheric and radiometric corrections
2. Masks: clouds, glint, land, deep water (create and inventory of posible mask algorithms for GEE). The images from Plante Scope have the "usable data mask", it includes striping out pixels by haze, shadows, snow or clouds. 
3. Depth Invariant Index (DII)

III. **Image classification**

Selection of a set of images for each scene. We need more than 1 image/year or period of time, then generate a final mosaic with the final classification.

_Note:_ _The final mosaic is a sum of pixels. For example, if four images were classified you can expect a final mosaic with pixel values ​​between 2-8, because the pixel value corresponding to seagrass is 2, and if that pixel is present in only one image, then that pixel appears in the final mosaic with a value of 2. If a pixel is present in four images, then it will have a value of 8 in the final mosaic. Therefore, if you put a value of 4 in the variable ‘number’ you will discard pixels that only appear once (less than 4); if you put a value of 6 you exclude pixels that appear twice (less than 6). In this way you help to ‘clean up’ the final mosaic a bit._

1. Select coastal, Blue, Green, Red, DII bands
2. Create vector processing classes: sand, seagrass, oyster beds, corals.
3. Sample bands with ground-truth dataset (70% training, 30% validation) 
4. Train SVM model and classify (other models?)
5. Get accuracies and Kappa coefficients

IV. **Post classification**

TBD

We are exploring the possibility to do all these process on GEE ( see Planet's GEE Delivery Integration API https://developers.planet.com/docs/integrations/gee/quickstart/) 


See Lizcano-Sandoval et al. 2022 https://doi.org/10.1016/j.ecss.2022.108134 



