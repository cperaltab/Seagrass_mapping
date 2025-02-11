TTI_Planet_SVMmodel calculation scripts in GEE [here](https://code.earthengine.google.com/a68fca9abf08b5be9c0af0ed8e82351e)

Working with sections of our AOI as Planet imagery provides the images "in chunks". Selected the best images from our image collection downloaded from Planet, and
according to the AOI representation and the presence of clouds.

Currently using images from 2023 because Planet didnt show newer images. We need to try to fin imsges for 2024.

We are using ground truth data from our field trip in January 2025. No seagrass patches were found but other features where identified. 
See comments in GEE script and habitat type occurrence dataset.

The field data collection showed the following classes: HardBottom, subaquaveg (macroalgae), mud, oyster, sand, shell. 
The field data also applies the classes as "HabitatType": soft bottom, Macroalgae-softbottom, hard bottom, Macroalgae-hardbottom, macroalgae, Macroalgae-mud, oyster bed, Softbottom-shell, mud-shell
The spatial resolution of the images doesent allow us to separate all these features, therefore we will merge as follow: 
- softbottom=>mud+sand:0
- hardbottom=>Hard Bottom + shell + oyster:1
- subaquaveg=>macroalgae:2

Not enougph data points were registered for macroalgae and oyster alone, therefore the classification for these specific fatures will be diffuclt to almost imposible.
What to do when having a point for hard bottom + macroalgae? try to see if we can separe hard bottom alone and hard bottom + macroalgae


