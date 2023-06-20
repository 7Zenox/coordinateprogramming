# Coordinate Programming
This repo is a collection of programs for data analysis around coordinates of locations. The geoencoder and reverse geoencoder used here in ArcGIS from geopy. Since the code has been programmed with Indian market's data, ArcGIS geoencoder from geopy has been used. The geoencoder has provided highest accuracy for a free to use geoencoder.

`Generalized Methodology`
- A coordinate is geoencoded using ArcGIS geoencoder
- The distance between original coordinates and geoencoded coordinates is calculated using Haversine formula below

$$
a = \sin^2(\frac{\Delta\varphi}{2}) + \cos \varphi_1 \cdot \cos \varphi_2 \cdot \sin^2(\frac{\Delta\lambda}{2})
$$

$$
c = 2 \cdot \text{atan2}(\sqrt{a}, \sqrt{1-a})
$$

$$
d = R \cdot c
$$

$$ Haversine\ Formula $$

- The calcualated distance is compared with a user input threshold to make appropriate filters
- A plot is generated on map using folium library to cross verify and visualize the results of the process.

`Coordinate Check`
- Uses URL ArcGIS geoencoder (this method is slower ~1 geoncoding/sec but provides extent of coordinates for improved cross-checking methods)
- This method uses 'naive' approach for geoencoding. It concatenates the all provided address related details like NAME, ADDRESS, AREA, CITY and PINCODE before geoencoding. The method is faster but may provide more anomalous data. 

`Coordinate Check Best Fit`
- Uses geopy ArcGIS geoencoder (this method is faster ~2-3 geoencoding/sec but does not provide extent)
- This method uses 'best fit' approach where it geoencodes the address with different level of details and finds the coordinates closes to the original coordinate for highest accuracy. This method requires significantly more time but can provide more accurate results when the task is one off.

`Coordinate Correction`
- Corrects the coordinates if the distance between original and geoencoded coordinates is greater than a certain threshold
- This notebook uses naive approach implementation.
