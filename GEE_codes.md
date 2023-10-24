# EVI-monitoring-GEE
// Testing a random region
var studyArea =  ee.Geometry.Polygon(
        [[[3.246980338791907, 45.835336025505995],
        [3.247881561020911, 45.83249544350292],
        [3.249383598069251, 45.83285426186172],
        [3.2479673917093876, 45.837279498073954],
        [3.2462507779398564, 45.837458892119855]]]);;
Map.addLayer(studyArea,{color:'green'},'Border');

//Cloud masking
function maskS2clouds(images) {
  var qa = images.select('QA60');
  var cloudBitMask = 1 << 10;
  var cirrusBitMask = 1 << 11;
  var mask = qa.bitwiseAnd(cloudBitMask).eq(0).and(qa.bitwiseAnd(cirrusBitMask).eq(0));
      
  return images.updateMask(mask).divide(10000).copyProperties(images).set('system:time_start', images.get('system:time_start'));
}


//Filter images from Sentinel 2
var images_filtered = ee.ImageCollection('COPERNICUS/S2_HARMONIZED')
  .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
  .filterDate('2015-01-01', '2022-12-31')
  //.filter(ee.Filter.calendarRange(0, 13,'month'))
  .filterBounds(studyArea)
  .map(maskS2clouds);

print(images_filtered);

// EVI calculation

var addEVI = function(image){
  
    var evi = image.expression('2.5* ((NIR - RED) / (1 + NIR + 6 * RED - 7.5 * BLUE))',
    { 'NIR': image.select('B8'),
      'RED': image.select('B4'),
      'BLUE': image.select('B2')});
    return evi.copyProperties(image, ['system:index', 'system:time_start']);
    
};
  
var addEVI = images_filtered.map(addEVI);  
print(addEVI);

var img_filtered_clip = images_filtered.first().clip(studyArea);
var nd = addEVI.first().clip(studyArea);


var chart = ui.Chart.image.seriesByRegion({
  imageCollection:addEVI, 
  regions:studyArea,
  reducer: ee.Reducer.mean(), 
  scale:10,
  seriesProperty:'class'
  
});

print(chart);
