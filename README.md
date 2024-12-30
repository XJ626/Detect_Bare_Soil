# Detect Bare Soil pixel in China
The code is for detecting the bare soil pixels using time-series images
## Background
Accurate and detailed spatial–temporal soil information is crucial for soil quality assessment worldwide, particularly in the countries with large populations and extensive agricultural areas. Using remote sensing technology to generate bare soil reflectance composites has been shown as a prerequisite for effectively modeling soil properties. However, most bare soil extraction methods rely on the single-period satellite imagery, making it difficult to produce a complete bare soil map. Although some developed methods have explored the advantages of multitemporal images, single indicators (e.g., Normalized Difference Vegetation Index and Normalized Burn Ratio 2) are prone to misidentifying bare soil as other land cover types such as impervious surface. Additionally, these methodologies were designed for specific areas and coarse spatial resolution images, leaving their generalizability to other areas or larger scales underexplored.
## Main idea
We proposed a Two-Dimensional Bare Soil Separation (TDBSS) framework to generate the bare soil composites of Chinese cropland at 10-m spatial resolution using multi-temporal Sentinel-2 images. This method employs the Normalized Difference Red/Green Redness Index and Soil Adjusted Vegetation Index as bidimensional indicators. We identified optimal thresholds for these indicators by analyzing ecoregion-specific samples and then implemented them across nine major agricultural zones in China. Additionally, we evaluated the framework against three prevalent bare soil extraction methods (i.e., Barest Pixel Composite, Soil Composite Mapping Processor, and Geospatial Soil Sensing System) based on spatial accuracy. 
## Main framework
This study aims to: (1) propose an effective method to distinguish vegetation (i.e., photosynthetically active areas of cropland, the same below), straw, and impervious surface from bare soil
by separating hidden information in two-dimensional space and determining thresholds with the confidence ellipse method, and generate a continuous bare soil map over China at 10-m spatial resolution; (2) make a comprehensive evaluation on three prevalent bare soil extraction algorithms (BPC, SCMaP and GEOS3) for their areal and spatial accuracy. The main process is as follows.
                                                      ![image](https://github.com/user-attachments/assets/f1903f50-6f8b-4507-82b2-fe4dcdd79648)
                                                                  Fig.1 The main workflow of TDBSS method and this study.
                                                                  
### Sentinel-2 image acquisition and treatments
Sentinel-2 Multi-Spectral Imager constellation includes two satellite sensors (2A and 2B), with a five-day revisiting period. It provides 13 spectral bands with different spatial resolution at 10 m, 20 m or 60 m. For the study area, the Level-2A products during the period from 1 January 2018 to 31 December 2022 were downloaded via Google Earth Engine. These products have been geometrically and radiometrically corrected. To acquire the high-quality images, the QA band was applied remove clouds and cirrus furtherly. Finally, we obtained the available cloud-free Sentinel-2 images, presenting an escalating pattern from the south towards the north. The six bands were used in this study for both the creation of true color composites and the calculation of various indices, covering the visible (B2-B4), NIR (B8), and SWIR (B11, B12) regions. All the bands were resampled to a 10-m spatial resolution using the bilinear method and projected into the WGS84 Geographic Latitude-Longitude system.
                                                      ![image](https://github.com/user-attachments/assets/c4b399b6-5b85-496f-93e0-320ae161a85c)
                                                    Fig.2 The image count of Sentinel-2 scenes used in the per pixel compositing for this study.
                                                    
### Geospatial soil sensing System
Geospatial Soil Sensing System (GEOS3) is a soil spectral reflectance extraction method proposed by Dematte et al. (2018), the procedure is as follows. The first step is to establish a time-series database of Sentinel-2 images from 2018 to 2022. Secondly, the database is filtered to remove pixels containing vegetation, straw, water, and other land covers that are not bare soil from each satellite image. The set of rules for this step was defined as follows: the Normalized Difference Vegetation Index (NDVI) was used to distinguish vegetation from bare soil areas and the spectral mixture of soil and vegetation due to the significant difference in values between them. According to the study by Dematte et al. (2018), we set the NDVI value between 0 and 0.25 as the threshold for soil, while the value for vegetation was greater than 0.25. Meanwhile, discriminating straw from soils in satellite images was achieved using the 0.15 threshold for Normalized Burn Ratio 2 (NBR2) (Dematte et al., 2018). To improve soil masking, the difference between B4 and B3, as well as between B3 and B2 were also calculated. The third step is to calculate the spectral reflectance for each soil pixel over the time series. Finally, the spectral reflectance for each soil pixel is filtered by the median value, composing a continuous soil spectral reflectance map.



# Reference:
[1] Xue J, Zhang X, Huang Y, et al. A two-dimensional bare soil separation framework using multi-temporal Sentinel-2 images across China[J]. International Journal of Applied Earth Observation and Geoinformation, 2024, 134: 104181.
[2] Demattê J A M, Fongaro C T, Rizzo R, et al. Geospatial Soil Sensing System (GEOS3): A powerful data mining procedure to retrieve soil spectral reflectance from satellite images[J]. Remote Sensing of Environment, 2018, 212: 161-175.
[3] Demattê J A M, Safanelli J L, Poppiel R R, et al. Bare earth’s surface spectra as a proxy for soil resource monitoring[J]. Scientific reports, 2020, 10(1): 4461.
[4] Diek S, Fornallaz F, Schaepman M E, et al. Barest pixel composite for agricultural areas using landsat time series[J]. Remote Sensing, 2017, 9(12): 1245.
[5] Sorenson P T, Shirtliffe S J, Bedard-Haughn A K. Predictive soil mapping using historic bare soil composite imagery and legacy soil survey data[J]. Geoderma, 2021, 401: 115316.
[6] Rogge D, Bauer A, Zeidler J, et al. Building an exposed soil composite processor (SCMaP) for mapping spatial and temporal characteristics of soils with Landsat imagery (1984–2014)[J]. Remote Sensing of Environment, 2018, 205: 1-17.

