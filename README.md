# P_xuthus
This repository intends to store a GIS exploratory data analysis exercise with data from an open access scientific paper and contains an R-based analysis of the spatial distribution of Papilio xuthus (an insect species), based on raw location data. The data is visualized using interactive maps to analyze the species' geographical spread.

Papilio_xuthusRawData.csv: Contains raw data of latitude and longitude coordinates for recorded Papilio xuthus observations.
R Scripts: The script used to process, visualize, and map the data (provided in this repository).

To run this analysis, ensure you have the following R packages installed:
sf: For handling spatial data.
leaflet: For interactive mapping.

Data Loading: The raw data is read from the CSV file:
data <- read.csv("Papilio_xuthusRawData.csv")

Data Inspection: The first few rows and structure of the data are checked using:
head(data)
str(data)

Spatial Data Conversion: The data is converted to a spatial object (simple features) using sf:
data_sf <- sf::st_as_sf(data, coords = c("longitude", "latitude"), crs = 4326)

Handling Missing Data: The number of missing latitude and longitude values is checked:
sum(is.na(data_sf$longitude))  
sum(is.na(data_sf$latitude))   

Map Visualization: An interactive map is created using the leaflet package:
leaflet(data_sf) %>%
addTiles(urlTemplate = "https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}.png") %>%
addCircleMarkers(
  popup = ~paste("<i>", species, "</i>"),
  color = "blue",
  radius = 6,
  fillOpacity = 0.7
) %>%
addLegend(
  position = "topright",
  title = "Species", 
  colors = c("blue"), 
  labels = c("Papilio xuthus"),
  opacity = 1
)
This produces a customized interactive map where markers represent the locations of Papilio xuthus. The basemap is light-toned with blue markers for a clear, aesthetically pleasing visualization.

Expected Output
An interactive map where the species name appears in a popup when clicking a marker and a legend that displays the species associated with the blue markers.

License
This project is licensed under the MIT License - see the LICENSE file for details.

GitHub HTML viewer link:
https://htmlview.glitch.me/?https://github.com/Amarah-boop/P_xuthus/blob/main/P_xuthus.html
