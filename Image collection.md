var hz = /* color: #d63000 */ee.Geometry.Point([91.80716934996961, 22.50901826053286]),
    geometry = 
    /* color: #ddffbc */
    /* displayProperties: [
      {
        "type": "rectangle"
      }
    ] */
    ee.Geometry.Polygon(
        [[[91.79715303126663, 22.5140037787229],
          [91.79715303126663, 22.502427072892615],
          [91.81792405787796, 22.502427072892615],
          [91.81792405787796, 22.5140037787229]]], null, false);

          var s2 = ee.ImageCollection("COPERNICUS/S2_SR_HARMONIZED") 
        .filterBounds(hz)
        .filterDate("2022-01-01", "2022-12-31")
        .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE',10))
        .max()
        print("Image collection",s2)
        
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

Map.addLayer(s2,{},"s2 collection")
