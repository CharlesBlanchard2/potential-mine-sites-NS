# potential-mine-sites-NS
Python notebook to create an interactive folium-based map of potential mine sites in Nova Scotia.

## Introduction
GeoPandas is a comprehensive Python library used to store, manipulate, and display spatial data. This allows for complex geospatial operations to be performed in Python that would otherwise require a spatial database (NumFOCUS, Inc., 2025d). The library was created as a spin-off of the popular library pandas, which stores tabular data in objects called dataframes, containing series objects as columns and provides functions to manipulate and analyze the data within them (NumFOCUS, Inc., 2024). 
GeoPandas expands on this via the introduction of the GeoDataFrame and GeoSeries data types. GeoDataFrames are simply a subclass of pandas dataframes with an integrated geometry column stored as a GeoSeries (subclass of pandas series) type object (NumFOCUS, Inc., 2025a). GeoSeries store geometry for features as Shapely objects, creating a vector (NumFOCUS, Inc., 2025b). With GeoDataFrames the GeoPandas library can then access other popular geospatial modules such as shapely for geometric operations, folium for interactive mapping, and pyogrio for accessing files (NumFOCUS, Inc., 2025d). This integration with other modules and its simple form of spatial data storage combine to make GeoPandas a popular and powerful tool for spatial analysis. 
In order to learn and explore GeoPandas I chose to recreate Assignment 3 from GISY 5004. This assignment consisted of scouting the suitability of potential mine sites in Nova Scotia by overlaying resource data consisting of counties, forest, and soils shapefiles with 5 sets of potential mine site point features (Appendix A). A frequency table was generated from the overlaid polygons and the final result was then styled and labelled appropriately to create a cartographic product in ArcGIS Pro (Appendix B). Originally, the processing for this assignment was accomplished using ArcGIS Pro ModelBuilder, but every step performed seemed to be possible to complete with GeoPandas, guiding my choice of problem. Additionally, I felt I could improve on a few aspects of the assignment, utilizing GeoPandas’ greater customization when it came to labelling and clustering of points. In order to accomplish my goal, I broke the project down into four main steps:
-	Store resource and site data as GeoDataFrames
-	Perform geoprocessing on this data
-	Generate a frequency table
-	Create an interactive map of mine sites with styling, tooltips, labels, and clustering
These steps will be detailed in the coming section of the report, followed by a summary of learning strategies, a discussion section, and references/appendices.
Storing Data as GeoDataFrames
This script begins by importing several spatial datasets—mine site locations and environmental resource layers (counties, forests, and soils)—as GeoDataFrames using the GeoPandas library (Appendix A). Each group of potential mine sites (FirstSites through FifthSites) was loaded individually, along with shapefiles representing natural resource information. These datasets were reprojected to a common coordinate reference system (UTM NAD83 Zone 20) to ensure accurate spatial analysis (Appendix C).
## Geoprocessing
Next, the script performed a series of geoprocessing tasks. Each set of mine sites was buffered based on a site-specific distance stored in the BUFF_DIST attribute. The resulting buffered geometries were plotted for visualization. All buffered site layers were then merged into a single GeoDataFrame, with a unique site ID added to distinguish between site groups. Spatial overlay operations were performed to intersect the buffered sites with the counties, forest types, and soil layers (Appendix D). These intersections helped identify the environmental and regulatory context of each potential mine site.
## Frequency Table
Following the geoprocessing, the script calculated a frequency table summarizing the intersected data. This included calculating the area of each intersected polygon in hectares and grouping the data by county, tree species, soil type, and stoniness to count occurrences and total area per category (Appendix B). The script also standardized tree species names and stoniness ratings using dictionary mappings for improved readability in the final legend (Colville et al., 2002).
## Interactive Map
Finally, an interactive map was created using the folium and folium.plugins libraries. Layers were styled to show dominant tree types and stoniness levels, each with its own symbology and legend. Tooltips displayed relevant attributes, such as site name, dominant tree, and soil type. A custom label system was built using marker clusters and styled pop-ups that summarize key characteristics of each site. Layer controls were added to allow users to toggle visibility of map elements. The final product was a detailed, interactive visualization of potential mine sites within their environmental and regulatory contexts (Appendix E).

## Appendices
### Appendix A - Input Datasets
All datasets exported as shapefiles from ArcGIS Pro using Data > Export Features.
-	NovaScotiaCounties (Counties GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/NovaScotiaCounties/FeatureServer
-	Coordinate System: NAD83(CSRS) / UTM Zone 20N
-	Courtesy of: Statistics Canada and Dave MacLean
-	NSForest_Pg (view) (Forest GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/NSForest_Pg_view/FeatureServer
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Nova Scotia Department of Lands and Forestry, Forestry Division and Dave MacLean
-	NSSoilsPg (view) (Soils GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/NSSoilsPg_(view)/FeatureServer
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Nova Scotia Department of Natural Resources and Renewables and Dave MacLean
-	Sites for First Location (FirstSites GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/Sites_for_First_Location/FeatureServer
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Dave MacLean
-	Sites for Second Location (SecondSites GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/Sites_for_second_location/FeatureServer 
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Dave MacLean
-	Sites for Third Location (ThirdSites GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/Sites_for_third_location/FeatureServer 
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Dave MacLean
-	Sites for Fourth Location (FourthSites GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/Sites_for_fourth_location/FeatureServer 
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Dave MacLean
-	Sites for Fifth Location (FifthSites GeoDataFrame)
-	https://services.arcgis.com/9PtzeAadJyclx9t7/arcgis/rest/services/Sites_for_fifth_location/FeatureServer 
-	Coordinate System: NAD_1983_UTM_Zone_20N
-	Courtesy of: Dave MacLean



### Appendix B - Frequency Table (First 12 Records)

COUNTY	Descriptio	SP1	HEIGHT	SOILNAME	STONINESS	Count	Total_Area_ha
Annapolis County	Annapolis Possible Site	BF	11	Bridgetown	2	1	1.90813
Annapolis County	Annapolis Possible Site	RM	13	Bridgetown	2	1	0.64928
Annapolis County	Annapolis Possible Site	RM	15	Bridgetown	2	1	0.75846
Annapolis County	Annapolis Possible Site	SM	18	Bridgetown	2	1	0.14183
Annapolis County	Annapolis Possible Site	SM	18	Horton	-	1	0.78403
Annapolis County	Annapolis Possible Site	US	4	Bridgetown	2	1	2.53982
Annapolis County	Annapolis Possible Site	US	4	Horton	-	1	0.27569
Colchester County	North Colchester Possible Site	BS	10	Pugwash	1	1	0.36585
Colchester County	North Colchester Possible Site	BS	13	Pugwash	1	2	1.48587
Colchester County	North Colchester Possible Site	BS	13	Stewiacke	0	2	0.82144
Colchester County	North Colchester Possible Site	EH	13	Pugwash	1	1	0.69931
Colchester County	North Colchester Possible Site	EH	13	Queens	1	1	0.49350


### Appendix C – Projections

Dataset Name	Original CRS	Reprojected CRS	Purpose of Reprojection
FirstSites–FifthSites	NAD_1983_UTM_Zone_20N (EPSG:26920)	No reprojection required	All mine site shapefiles already in correct CRS
Counties	NAD83(CSRS) / UTM Zone 20N (EPSG:2961)	Reprojected to EPSG:26920	Aligned for intersection with site buffers
Forest	NAD_1983_UTM_Zone_20N (EPSG:26920)	Confirmed/reprojected to EPSG:26920	Ensures accuracy for overlay and area calculations
Soils	NAD_1983_UTM_Zone_20N (EPSG:26920)	Confirmed/reprojected to EPSG:26920	Ensures accuracy for overlay and area calculations
SiteLabels (Centroids)	NAD_1983_UTM_Zone_20N (EPSG:26920)	Reprojected to WGS 84 (EPSG:4326)	Needed for latitude/longitude input for labels in folium map

Note: Reprojection was performed using the .to_crs() method in GeoPandas. The SiteLabels dataset was the only layer reprojected to a geographic coordinate system (EPSG:4326) because Folium requires all coordinates for marker placement to be in latitude/longitude format.



### Appendix D - Intermediate Datasets
-	AllSites GeoDataFrame
-	Created using pandas.concat() to merge all site GeoDataFrames together
-	SiteCounties, SiteForest, and SiteSoils GeoDataFrames
-	Created by intersecting AllSites with each dataset using .overlay() function
-	IntersectedSites GeoDataFrame
-	Created by intersecting AllSites with SiteForest, SiteCounties, and SiteSoils
-	freq_table Table
-	Created by using .groupby() and .agg() functions to make frequency table
-	SiteLabels GeoDataFrame
-	Created by using copy.deepcopy() function to copy IntersectedSites for labelling

### Appendix E - Final Interactive Map Screen Capture



### Appendix F – Software Versions
-	Visual Studio Code 1.99.2
-	Python 3.13.1
-	GeoPandas 1.0.1
-	Folium 0.19.5
