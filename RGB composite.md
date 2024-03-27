var geometry = 
    /* color: #d63000 */
    /* displayProperties: [
      {
        "type": "rectangle"
      }
    ] */
    ee.Geometry.Polygon(
        [[[91.7625121195153, 22.538917659617134],
          [91.7625121195153, 22.470407179727914],
          [91.86001578162468, 22.470407179727914],
          [91.86001578162468, 22.538917659617134]]], null, false);
var s2 = ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED") 
        .filterBounds(hz)
        .filterDate("2022-01-01", "2022-12-31")
        .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',10))
        
        print(s2)
        
var img = ee.Image("COPERNICUS/S2_SR_HARMONIZED/20220108T042139_20220108T043143_T46QCK")
          .clip(geometry)
print(img)
var capturingDate = ee.Date(img.get("system:time_start"))
print(capturingDate)
var formattedDate = capturingDate.format("YYYY-MM-dd");
print(formattedDate)

var vizParams = {
  bands: ["B4", "B3", "B2"],

min: 278,
max: 1810
}
Map.addLayer(img,vizParams,"raster image")
