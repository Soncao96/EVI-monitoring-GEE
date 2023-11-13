# EVI-monitoring-GEE
The enhanced vegetation index (EVI) is an 'optimal' vegetation index that decouples 
the canopy background signal and reduces atmospheric impacts to improve the vegetation signal with greater sensitivity in high biomass regions and improved vegetation monitoring.

# Objective
To retrieve and monitor EVI values of a certain region of interest for a period of time using Sentinel 2 images 


# Enhanced Vegetation Index (EVI) Formula:
EVI = G * ((NIR - R) / (NIR + C1 * R – C2 * B + L))   or
EVI (Sentinel 2) = 2.5 * ((B8 – B4) / (B8 + 6 * B4 – 7.5 * B2 + 1)).
