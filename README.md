# EVI-monitoring-GEE
The Enhanced Vegetation Index (EVI) is a satellite-derived index designed to optimize the vegetation signal while minimizing soil and atmospheric influences, such as aerosol scattering. EVI improves upon the Normalized Difference Vegetation Index (NDVI) by reducing sensitivity to atmospheric conditions and enhancing the response in areas with dense vegetation cover. It achieves this by adding coefficients that account for atmospheric resistance and canopy background effects.

# Objective
To retrieve and monitor EVI values of a certain region of interest for a period of time using Sentinel 2 images 

# Enhanced Vegetation Index (EVI) Formula:
EVI = G * ((NIR - R) / (NIR + C1 * R – C2 * B + L))   or
EVI (Sentinel 2) = 2.5 * ((B8 – B4) / (B8 + 6 * B4 – 7.5 * B2 + 1)).
