# Forty Years of Satellite Imagery Reveal a Connection Between Wetness Changes in the Arctic and Permafrost Degradation

The effects of a changing climate are evident across the globe. In particular though, the Arctic is seeing a vast and rapid rise in temperature upwards of 3°C since the industrial revolution, according to the Intergovernmental Panel on Climate Change's 2018 special report [1]. The implications for such a drastic warming shift in the arctic are obvious at first glance. Permafrost (ground that stays below freezing for at least two years) degradation is clearly visible in the form of vast expanses of polygonal terrain in the far north.

![Map of estimated warming accross the globe - IPCC 2022](https://github.com/rbiessel/ArcticWetness/blob/main/images/warming_IPCC2022.png?raw=true)
_Map of warming accross the globe from the International Panel on Climate Change's 2018 special report._

During the pleistocene, large wedges of ground ice formed in these arctic regions. Gradually growing, the ice pushes the ground apart, propagating upwards as more glacial sediment is deposited over top. Now, these ice wedges have switched from growth to thaw near the surface. The melt of ice has left depressions in the form of a web of polygons across much of the north slope. In some instances, this kind of permafrost degradation has advanced to a degree where many such polygons eventually sink far enough into the ground that the landscape turns into a dotted tapestry of thermokarst lakes.

![Permafrost high-center polygons](https://i0.wp.com/eos.org/wp-content/uploads/2022/01/permafrost-polygons.jpg?w=1200&ssl=1)
_An example of ice-wedge polygons. Photo credit: Christian Andresen_

This kind of permafrost thaw is not surprisingly terrible for any kind of infrastructure, but what’s less obvious and less well understood is permafrost thaw’s more far-reaching (and much less visible) consequences. While these ice wedges have been forming and the collecting sediment, this kind of soil has also been collecting the remains of plants and other organic matter. In other words, the arctic permafrost has generally been a carbon sink. With new thaw of permafrost however, this previously stored carbon is at risk of returning to the atmosphere in the form of greenhouse gasses like carbon dioxide and methane. In fact arctic permafrost contains up to 1/3 of the globe’s soil carbon [2], [3].

With the concern of accelerated greenhouse gas emission by thawing permafrost, it is increasingly advantageous to gauge where and how much permafrost may be thawing. How does water and “wetness” factor into this though? In addition to permafrost being closely coupled with the carbon cycle, it’s also closely coupled with the water cycle. First, thaw of ice-rich permafrost is going to release water. This top-down thaw then preferentially increases the water content near the surface and prevents water from draining. Similarly, the polygons formed by thawing ice-wedges tend to collect water. If this water collects enough, it also tends to increase the rate of thaw of adjacent permafrost. Thermokarst lakes further accelerate thaw [4]. In addition, a change in moisture is an important parameter for other processes, like the decomposition of the stored carbon (the process that actually releases carbon in gas form) [5] and how much heat is actually absorbed by the ground instead of being used to evaporate water [6].

This only a brief snapshot of how wetness may be of interest to climate research at large. In this analysis, I try and relate changes in wetness to surface expressions of permafrost. In other words, can satellite imagery help identify the most at-risk parts of the northern tundra? The rest of this blog explores a 40-year dataset of Landsat imagery to answer this question. In short, this study suggests yes -- it appears that we can identify the areas where the surface is getting both wetter and drier, and where existing permafrost degradation is expanding. The resulting moisture trends tend to correlate strongly with visible permafrost features.

## Remotely Sensed Observations: Landsat 5 and Landsat 8

Landsat is a series of NASA satellites equipped with multispectral imagers. These kinds of sensors are like advanced cameras, taking pictures of not only just the red, green, and blue light reflected off the earth, but also light in other parts of the spectrum that our eyes alone can’t observe. This means that we can use this type of imagery to sometimes characterize processes that are invisible to the naked eye and do so at large scales.

Landsat 5 collected imagery between 1984 and 2013 while Landsat 8 has collected imagery from 2013 to the present. This equates to about 40 years of data that went into this analysis. The challenging part of this kind of imaging of the arctic, however, is frequent cloud cover. To avoid snow-covered ground, I only included images acquired between June 15th and August 15th. Now-adays, this kind of use of remotely sensed imagery is incredibly easy with Google Earth Engine, which can handle large volumes of data without needing to download it.

### Cloud Masking

Clouds represent a significant barrier to optical remote sensing in the arctic. To reduce their impact, I used the quality assurance information included with these images to perform a pixel-by-pixel mask of clouds and their shadows. This mask is not perfect, however, and this quality assurance pixel provided with the image does not identify more transparent clouds.

### "Wetness" and the Tasseled Cap Transformation

The tasseled cap transformation dates to 1976 with the first Landsat satellite [7]. It represents a series of weights that are used to transform the observed reflectance at each spectral (blue, red, green, infrared, etc.) band to a new reference frame that conveys more physical meaning and allows for much easier interpretation of the data. This kind of transformation condenses the information across the red, green, blue, and infrared observations into bands that describe “brightness”, “greenness”, and “wetness”. Numerous papers have been published deriving these weights for various platforms. In this study, I used weights derived by Crist & Cicone [8], for the Landsat 5 data and Baig et al [9] for Landsat 8 data and focus on the ”wetness” metric.

### Estimating Rates of Change

Having generated a wetness time-series, I now wanted to quantify how that metric has changed, pixel-by-pixel, for both Landsat 5 and Landsat 8 data. Because these two platforms have different sets of tasseled cap coefficients and different ranges, I separated the time-series and sought to estimate two separate rates for these two time-periods. As I mentioned earlier, the cloud mask didn’t perform perfect, which left residual transparent clouds. These clouds appear as anomalously high regions of wetness, and these have the potential to severely bias the rate estimates. The most common form of linear regression, least squares, suffered significantly from this bias. I chose then to fit a line to this data using a Theil-Sen estimator. This kind of regression is much less sensitive to outliers and works by computing the slopes between every pair of points, and then selecting the median.

## Results

The final estimates of wetness trend reveal quite interesting patterns regarding permafrost degradation. The figures below have been generated using these methods and illsustrate these wetness trends for two characteristic sites. In a GIS software I’ve overlaid the output wetness rates with Bing’s Aerial imagery base-layer. Red pixels represent large magnitude wetness rates while blue pixels indicate a decrease in wetness or drying trend. Pixels with near-zero slopes are displayed as transparent so that the underlying permafrost features are more visible. On their own, the magnitudes of these trends aren’t too meaningful, but in relation to nearby pixels, they can indicate relative trends. Comparing these trend magnitudes between the Landsat 5 and Landsat 8 datasets are even more difficult, but changes in how each of these rates are distributed spatially at local scales still has the potential to reveal insights about how near-surface permafrost thaw is evolving.

### Site A

In this first site, a variety of permafrost features are visible. A beaded stream cuts across the image from the northeast to the southwest. On either side are more streams and tundra that appears to have streaks in it which suggest they experience frequent water flow. Furthermore, some of these hydrologic features show evidence of permafrost degradation: a speckled pattern which on closer look are ice-wedge polygons. In both datasets, there is a clear relationship between higher magnitude wettening rate and this kind degraded tundra. Interestingly, in some of these regions, the trend switches from getting wetter to getting drier at the centers of the most degraded looking ground.

![Site A Basemap](https://github.com/rbiessel/ArcticWetness/blob/main/images/siteA_bingAerial.jpg?raw=true)
_Site A: Base imagery (Bing Aerial Basemap)_

![Landsat 5 derived wetness trends](https://github.com/rbiessel/ArcticWetness/blob/main/images/siteA_LS5toa.jpg?raw=true)
_Site A: Landsat 5 -- 1984 to 2013_

![Landsat 8 derived wetness trends.](https://github.com/rbiessel/ArcticWetness/blob/main/images/site_A_ls8TOA.jpg?raw=true)
_Site A: Landsat 8 -- 2013 to 2022_

### Site B

This second site is especially interesting because in 2007, a fire burned the southern half of this scene. This boundary is extremely obvious in the Landsat 5 wetness rate where the magnitudes are highest. Once again, these regions also coincide with highly polygonal terrain. In the Landsat 8 dataset, the wettening trends tend to switch from the flatter polygonal terrain to the adjacent hillsides and the edges of the thermokarst lakes. In addition, the more obviously degraded tundra has switched to a drying trend.

![Site B Basemap](https://github.com/rbiessel/ArcticWetness/blob/main/images/siteC_basemapjpg.jpg?raw=true)
_Site B: Landsat 8 -- 2013 to 2022_

![Site B Landsat 5 derived wetness trends](https://github.com/rbiessel/ArcticWetness/blob/main/images/siteC_LS5_TOA.jpg?raw=true)
_Site B: Landsat 5 -- 1984 to 2013_

![Site B Landsat 8 derived wetness trends](https://github.com/rbiessel/ArcticWetness/blob/main/images/siteC_LS8_TOA.jpg?raw=true)
_Site B: Landsat 8 -- 2013 to 2022_

### Conclusions

The mechanism for these trends likely needs more exploration but the obvious explanation for a positive trend is an increase permafrost thaw near the surface increases which increases the saturation of the soil and increases the amount of area covered by water. It’s less clear how the drying trends arise. It’s possible that significant permafrost thaw allows has allowed more shrubby vegetation to grow, blocking the view of the surface beneath it. It’s also possible that enough thaw has occurred to allow water to drain downwards more freely. The other possibility is that some of these smaller magnitude trends are just the result of random variation. Regardless of the specific mechanism, the correlation between these wettening trends and visible permafrost is intriguing and suggests this a promising method of monitoring permafrost from space and gauging changes in surface water content at a large scale.

## References

[1] M. Allen, O. P. Dube, W. Solecki, F. Aragón–Durand, W. Cramer, S. Humphreys, M. Kainuma, J. Kala, N.
Mahowald, Y. Mulugetta, R. Perez, M. Wairiu, K. Zickfeld, 2018, Framing and context supplementary material. In:
Global warming of 1.5°C. An IPCC Special Report on the impacts of global warming of 1.5°C above preindustrial levels and related global greenhouse gas emission pathways, in the context of strengthening the
global response to the threat of climate change, sustainable development, and efforts to eradicate poverty [V.
Masson-Delmotte, P. Zhai, H. O. Pörtner, D. Roberts, J. Skea, P.R. Shukla, A. Pirani, W. Moufouma-Okia, C.
Péan, R. Pidcock, S. Connors, J. B. R. Matthews, Y. Chen, X. Zhou, M. I. Gomis, E. Lonnoy, T. Maycock, M.
Tignor, T. Waterfield (eds.)]. In Press.

[2] G. Hugelius et al., “Estimated stocks of circumpolar permafrost carbon with quantified uncertainty ranges and identified data gaps,” Biogeosciences, vol. 11, no. 23, pp. 6573–6593, Dec. 2014, doi: 10.5194/BG-11-6573-2014.

[3] E. A. G. Schuur et al., “Climate change and the permafrost carbon feedback,” Nat. 2015 5207546, vol. 520, no. 7546, pp. 171–179, Apr. 2015, doi: 10.1038/nature14338.

[4] T. P. Wellman, C. I. Voss, and M. A. Walvoord, “Impacts of climate, lake size, and supra- and sub-permafrost groundwater flow on lake-talik evolution, Yukon Flats, Alaska (USA),” Hydrogeol. J., vol. 21, no. 1, pp. 281–298, Feb. 2013, doi: 10.1007/S10040-012-0941-4/FIGURES/5.

[5] D. M. Lawrence, C. D. Koven, S. C. Swenson, W. J. Riley, and A. G. Slater, “Permafrost thaw and resulting soil moisture changes regulate projected high-latitude CO 2 and CH 4 emissions,” Environ. Res. Lett, vol. 10, p. 94011, 2015, doi: 10.1088/1748-9326/10/9/094011.

[6] J. van Huissteden, “The Energy Balance of Permafrost Soils and Ecosystems,” Thawing Permafr., pp. 51–106, 2020, doi: 10.1007/978-3-030-31379-1_2.

[7] R. J. Kauth and G. S. Thomas, “Purdue e-Pubs The Tasselled Cap-A Graphic Description of the Spectral-Temporal Development of Agricultural Crops as Seen by LANDSAT,” 1976, Accessed: Apr. 25, 2022. [Online]. Available: http://docs.lib.purdue.edu/lars_symphttp://docs.lib.purdue.edu/lars_symp/159.

[8] E. P. Crist and R. C. Cicone, “A Physically-Based Transformation of Thematic Mapper Data—The TM Tasseled Cap,” IEEE Trans. Geosci. Remote Sens., vol. GE-22, no. 3, pp. 256–263, 1984, doi: 10.1109/TGRS.1984.350619.

[9] M. H. A. Baig, L. Zhang, T. Shuai, and Q. Tong, “Derivation of a tasselled cap transformation based on Landsat 8 at-satellite reflectance,” Remote Sens. Lett., vol. 5, no. 5, pp. 423–431, May 2014, doi: 10.1080/2150704X.2014.915434.
