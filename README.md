# GEE
 Google Earth Engine Scripts fro SERVIR


Simply copy and paste the following into the script window (center of Google Earth Engine). Otherwise find the scripts dowload from GEE in the "Scripts" directory.  The local assets used in this tutorial are in "Assets" directory and should be uploaded into you GEE "Assets" that are accessible in the GEE "Assets" tab.
The GEE "Imports" lines, which include defining the FeatureCollection, must be generated within GEE manually using the "Geometry Imports" menu at the bottom of the GEE inteface.
The "basins" GEE Table is the "regions_inclusive" asset found in the directory "Assets" and should therefore be uploaded. Otherwise, you can upload your own shapefile into GEE.
The "Imports" as used in tutorial video is shown in file README_Imports.md.
// This code produces a land cover classification base on either a shapefile or a collection of mygee from GEE.
// The shapefile is created with a GIS and must contain an attribute called "class_id" which is a number starting at 0 (zero).
// The GEE collection are mygee collected with the "Add Marker" and "Geometry imports" button on the GEE image diplay.

//Map.centerObject(mygee, 11); //centers map near point collection
Map.setCenter(-58.5, 7.4, 11); //center around Georgetown, Guyana with zoom level 9

// the following variable that I called "mygeeclasses" is a merge of all classes you have defined with the GEE interface.  
// If you have a shpaaefile instead, you do not need to use the following line and can comment it out with double slash. ie. //

var mygeeclasses = RedMangroves.merge(BlackMangroves).merge(Water).merge(Forest).merge(Wetlands).merge(Agriculture).merge(MudFlat)
// Use these bands for prediction.
var bands = ['B2', 'B3', 'B4', 'B5', 'B6', 'B7', 'B10', 'B11','HV','s1vh','sB3','sB4','sB5'];  // here you can specify which Landsat bands, ALOS and Sentinel-1 bands as well

////Here I arrange and display uploade bands from Sentinel-2 mosaic hub

var S2hubVis = {
  bands: ['sB5', 'sB4', 'sB3'],
  min: 10,
  max: 30
};

var S2hub = S2B03.clip(basins);
S2hub = S2hub.addBands(S2B04);
S2hub = S2hub.addBands(S2B05);
S2hub = S2hub.rename(['sB3','sB4','sB5']);

Map.addLayer(S2hub, S2hubVis, 'Sentinel-2 Mosaic Hub');


///////  Next we load the Landsat, Sentinel-1 and ALOS/PALSAR data/////

// Make a cloud-free Landsat 8 TOA composite (from raw imagery).
var l8 = ee.ImageCollection('LANDSAT/LC08/C01/T1');

// limit collection to the landsat images that cover our region of interest,ie. 'basins' , for year 2018
var l8image = ee.Algorithms.Landsat.simpleComposite({
  collection: l8.filterDate('2017-01-01', '2017-12-31').filterBounds(basins),
  asFloat: true
});

l8image = l8image.clip(basins);


/// generate Sentine-1 average of VH polarization data for 2018.
// Sentinel-1 is from the European Space Agency (ESA) and operates at C-band in VV and VH polarization.
// VH or HV are more sensitive to volume and plants.  VV is about roughness such as surface waves on water.
var pol = 'VH';

// Define start and end dates to compile the Sentinel-1 collections\
// Each start/end pair are the periods over which to calculate each mean image to be differenced\
// yyyy-mm-dd
var start = '2017-09-01';
var end = '2017-10-31';

// Define resolution, will also be used to define the output resolution\
// The possible resolutions are 10, 25, or 40 meters
var res = 10;

var collection = ee.ImageCollection('COPERNICUS/S1_GRD')
  .filterBounds(basins)
  .filterDate(start, end)
  .select(pol);

//Compute the mean of the Sentinel-1 data collection over the period specfied above by start and end. 
//Then rename that band as 's1vh' so we can call and access it directly later
var S1_VH_mean = collection.reduce(ee.Reducer.mean()).rename('s1vh');

//Now, let's display the Sentinel-1 image
var s1Vis = {
  min: -20,
  max: -5,
};

S1_VH_mean = S1_VH_mean.clip(basins);

//The Map.addLayer simply displays the image with the visualization parameters specfied above and inserted in command below.
// Let's called that displayed image as 'Sentinel-1 VH'
//Map.addLayer(S1_VH_mean, s1Vis, 'Sentinel-1 VH');

//  Now add that Sentinel-1 mean backscksatter to the stack of Landsat bands with the following command:
var allimages = l8image.addBands(S1_VH_mean);

/////////////////////// Now, lets' add ALOS/PALSAR mosaics from JAXA. ///////////////////////////////////////////////
//////////// These are produced every year by JAXA. This is L-band data at HV and HH ////

var alos = ee.Image('JAXA/ALOS/PALSAR/YEARLY/SAR/2017');

//  compute the HV/HH ratio and add as new Band
var hvhh = alos.expression(
  '(HV/HH)', {
    'HH': alos.select('HH'),
    'HV': alos.select('HV')
}).rename('HVHH');

var alos = alos.addBands(hvhh);

// apply: γ₀ = 10log₁₀(DN²) - 83.0 dB
var DN = alos.select('HH');
var HVdB = DN.pow(2).log10().multiply(10).subtract(83);
HVdB = HVdB.rename(['HV'])  /// naming that band 'HV' for calling later


var alosHVVis = {
  min: -20,
  max: -5,
};
HVdB = HVdB.clip(basins);


//// Classification steps with landsat 8 and other images/////


var allimages = allimages.addBands(HVdB); // This line adds the HVdB ALOS image to the stack of bands including landsat
var allimages = allimages.addBands(S2hub); // This line adds the HVdB ALOS image to the stack of bands including landsat


// This property stores the land cover labels as consecutive
// integers starting from zero.
var label = 'class_id'
// Overlay the  on the imagery to get training data. That is the value of each band in the variable 'bands' above are
var training = allimages.select(bands).sampleRegions({
  collection: mygeeclasses,  ///set this equal to the training data you wish to use mygeeclasses or mygee or what ever else you have defined.
  properties: [label],
  scale: 30
});
print(label,training)


// Train a CART classifier with the above training data, labels and the bands. You can see the values for each training pixel
// in the 'Console' window on the right because it was printed in the line above.
var trained = ee.Classifier.smileCart().train(training, label, bands);

// Classify the image with the same bands used for training. 'tained' is the actual decision tree model and can be applied to the
// entire image
var classified = allimages.select(bands).classify(trained);  //'classified' is my new classification map

// Display the inputs and the results.

// the following is simply for setting associating each class_id to HTML color code. You should change those, add or remove items if you
// have more or less classes.  you can select your favorite colors by copy/paste the code from here https://htmlcolorcodes.com/
var mypalette=[  'red', // Red mangrove 0
  'black', // Black mangrove 1
  'blue', //  water (2)
  'green',  // forest 3
  'yellow', // agriculture 4
  'cyan', //wetlands 5
  '863e12'  // mud flat 6
]



//Map.addLayer(HVdB, alosHVVis, 'ALOS HV');

//Map.addLayer(allimages, {bands: ['B4', 'B3', 'B2'], max: 0.25}, 'Landsat 8 for 2017');  // This line displays an image composite of landsat bands B4,B3,b2 in 'allimages'

//Map.addLayer(allimages, {bands: ['s1vh'], min: -20, max:-5}, 'Sentinel-1 VH again');

Map.addLayer(classified, //displaying the classification map
             {min: 0, max: 6, palette: mypalette},  // using my choice of color for each class
             'Classification'); // call this layer 'classification
             
//the following export the classificaiton map 'classified' to your Google drive.
Export.image.toDrive({
  image: classified,
  description: 'classif',
  region: basins,
  fileFormat: 'GeoTIFF',
  scale: 30
});

