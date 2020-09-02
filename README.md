# GEE
 Google Earth Engine Scripts fro SERVIR


Simply copy and paste the following into the script window (center of Google Earth Engine). Otherwise find the scripts dowload from GEE in the "Scripts" directory.  The local assets used in this tutorial are in "Assets" directory and should be uploaded into you GEE "Assets" that are accessible in the GEE "Assets" tab.
The GEE "Imports" lines, which include defining the FeatureCollection, must be generated within GEE manually using the "Geometry Imports" menu at the bottom of the GEE inteface.
The "basins" GEE Table is the "regions_inclusive" asset found in the directory "Assets" and should therefore be uploaded. Otherwise, you can upload your own shapefile into GEE.
The "Imports" as used in tutorial video is shown in file README_Imports.md.

Next is the script that corresponds to "Classif_l8_S1_S2_Alos".  Further below is the script for "DataAnalysis".

// Classif_l8_S1_S2_Alos
//This code produces a land cover classification base on either a shapefile or a collection of mygee from GEE.
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


// This is the script for DataAnalysis

/**** Start of imports. If edited, may not auto-convert in the playground. ****/
var landsat8 = ee.ImageCollection("LANDSAT/LC08/C01/T1_SR"),
    sentinel2 = ee.ImageCollection("COPERNICUS/S2"),
    Guyana = ee.FeatureCollection("users/echoparkrs/region2_inclusive");
/***** End of imports. If edited, may not auto-convert in the playground. *****/
//center map
Map.setCenter(-58.6, 7.5);
Map.setZoom(10)
Map.centerObject(Guyana,7)
Map.setOptions('satellite')

var l8_res = 30;
var S2_out_res = 10;

print(Guyana,'Guyana Region 2')
Map.addLayer(Guyana,{},'Regions 2')

////////////////////
//Landsat 8///////
///////////////////

//filter collection
var landsatguyana = landsat8.filterDate('2017-07-15', '2019-10-30')
                           .filterBounds(Guyana)
                           .filter(ee.Filter.calendarRange(7,10,'month'))

                           
print(landsatguyana,'landsatguyana')


///Function definitions
function addNDVI(img) {
  img = ee.Image(img)
  var ndvi = img.normalizedDifference(['B5', 'B4']).rename(['ndvi'])
  var img_ndvi = img.addBands(ndvi)
  return img_ndvi
}

//add ndwi
function addNDWI(img) {
  img = ee.Image(img)
  var ndwi = img.normalizedDifference(['B3', 'B5']).rename(['ndwi'])
  var img_ndwi = img.addBands(ndwi)
  return img_ndwi
}


//cloudmask
function cloudMask(img){
  // Bits 3 and 5 are cloud shadow and cloud, respectively.
  var cloudShadowBitMask = (1 << 3)
  var cloudsBitMask = (1 << 5)
  // Get the pixel QA band.
  var qa = img.select('pixel_qa')
  // Both flags should be set to zero, indicating clear conditions.
  var mask = qa.bitwiseAnd(cloudShadowBitMask).eq(0)
                 .and(qa.bitwiseAnd(cloudsBitMask).eq(0))
  return img.updateMask(mask)
}


// this will compute ndvi forom the landsatguyana imagecollection
var l8guyana_ndvi = landsatguyana.map(addNDVI).map(cloudMask)
var l8guyana_ndwi = landsatguyana.map(addNDWI).map(cloudMask)


var imageVisParams_l8 = {"opacity":1,"min":-0.3,"max":1, "gamma":1};

//clip image collection to Guyana geometry\
var l8guyana_ndvi_final = l8guyana_ndvi.map(function(image) { return image.clip(Guyana); });
var l8guyana_ndwi_final = l8guyana_ndwi.map(function(image) { return image.clip(Guyana); });

//Map.addLayer(l8guyana_final.mean(),imageVisParams_l8,'L8 NDVI 2019')

//trying index and improve filtering
var l8_NDVI = l8guyana_ndvi_final.select(['ndvi']);
var l8_NDVI = l8_NDVI.median();
var l8_NDWI = l8guyana_ndwi_final.select(['ndvi']);
var l8_NDWI = l8_NDWI.median();

Map.addLayer(l8_NDVI,imageVisParams_l8,'L8 NDVI 2019')

////////////////////////////\
// Sentinel 2//////////////\
///////////////////////////\

//filter S2 imagery
var sentinelguyana = sentinel2.filterDate('2019-08-01', '2019-09-15')
                           .filterBounds(Guyana)
                           
print(sentinelguyana,'sentinelguyana')

//cloudmask
var maskcloud1 = function(image) {
var QA60 = image.select(['QA60']);
return image.updateMask(QA60.lt(1));
};

function maskS2clouds(image) {
  var qa = image.select('QA60');

  // Bits 10 and 11 are clouds and cirrus, respectively.
  var cloudBitMask = 1 << 10;
  var cirrusBitMask = 1 << 11;

  // Both flags should be set to zero, indicating clear conditions.
  var mask = qa.bitwiseAnd(cloudBitMask).eq(0)
      .and(qa.bitwiseAnd(cirrusBitMask).eq(0));

  return image.updateMask(mask).divide(10000);
}


// Function to calculate and add an NDVI band
var addNDVI = function(image) {
return image.addBands(image.normalizedDifference(['B8', 'B4']));
};

// Function to calculate and add an NDWI band
var addNDWI = function(image) {
return image.addBands(image.normalizedDifference(['B3', 'B5']).rename('ndwi'));
};

// Compute the EVI using an expression. return EVI.
var addEVI = function(image) {
return image.expression(
    '2.5 * ((NIR - RED) / (NIR + 6 * RED - 7.5 * BLUE + 1))', {
      'NIR': image.select(['B8']),
      'RED': image.select(['B4']),
      'BLUE': image.select(['B2'])
})};

// Add NDVI band to image collection

var sentinelguyana = sentinelguyana
                  .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
                  .map(maskS2clouds);
                  
var S2 = sentinelguyana.map(addNDVI).map(maskcloud1);
//var NDVI = sentinel2.map(addNDVI);
var S2 = S2.map(function(image) { return image.clip(Guyana); });
// Extract NDVI band and create NDVI median composite image
var NDVI = S2.select(['nd']);  //nd
var NDVI = NDVI.median();

var S2 = S2.map(addNDWI);
//var NDWI = NDWI.map(function(image) { return image.clip(guyana); });
var NDWI = S2.select(['ndwi']);
var NDWI = NDWI.median();

var S2EVI = sentinelguyana.map(addEVI);
//var EVI = S2EVI.select(['ev']);
var EVI = S2EVI.median();
var EVI = EVI.clip(Guyana);


var S2_NIR = sentinelguyana.select(['B8']);
var S2_NIR = S2_NIR.median();
var S2_NIR = S2_NIR.clip(Guyana);


// Create palettes for display of NDVI\
//var ndvi_visParams_s2 = {"opacity":1,"bands":['nd'],"min":0.03227182477712631,"max":0.12915651500225067, palette:['blue','white','green']};
var ndvi_visParams_s2 = {min: -1, max: 1};


// Display NDVI results on map
Map.addLayer(NDVI,ndvi_visParams_s2, 'S2 NDVI 2019');


//Exportig data to google Drive///
var geometry = ee.Geometry(Guyana)
Export.image.toDrive({
  image: NDVI,
  description: 'S2_NDVI_Aug2019',
  region: Guyana,
  fileFormat: 'GeoTIFF',
  scale: S2_out_res,
  maxPixels: 110315250
});

Export.image.toDrive({
  image: NDWI,
  description: 'S2_NDWI_Aug2019',
  region: Guyana,
  fileFormat: 'GeoTIFF',
  scale: S2_out_res,
  maxPixels: 110315240
});

Export.image.toDrive({
  image: EVI,
  description: 'S2_EVI_Aug2019',
  region: Guyana,
  fileFormat: 'GeoTIFF',
  scale: S2_out_res,
  maxPixels: 110315240
});

Export.image.toDrive({
  image: S2_NIR,
  description: 'S2_NIR_Aug2019',
  region: Guyana,
  fileFormat: 'GeoTIFF',
  scale: S2_out_res,
  maxPixels: 110315240
});



