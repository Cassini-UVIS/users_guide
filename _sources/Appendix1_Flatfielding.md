# Methods for Obtaining Flatfield Corrections

> Andrew Steffl

The easiest way to derive a flatfield correction is to illuminate the detector with a spatially-uniform monochromatic source. 
In this case, any differences in the number of counts in the individual detector pixels are the result of spatial (pixel-to-pixel) variations in the detector sensitivity (assuming that the signal to noise ratio is large). 
However,the presence of a grating in the UVIS optical path means that while the entrance slit may be evenly illuminated, only a small fraction of the detector --- the projected width of the slit on the detector divided by the length of the detector, or 3% for the UVIS occultation slits --- will be illuminated by a monochromatic source. 
This problem can be solved by using a spatially uniform white-light (equal intensity at all wavelengths) source to illuminate the entrance slits.
After dividing the resulting image by the instrument sensitivity as a function of wavelength (also referred to as the detector calibration curve) any pixel variations are due to variations in detector sensitivity. 
Sadly though, no such source exists. 
The next best thing is to use a spatially uniform source with a known spectrum. 
Then, after dividing the raw image by the detector calibration curve and the known spectrum, one can use the pixel to pixel variations to derive a flatfield correction.
Ideally, UVIS would have been taken to a synchrotron radiation facility and the beam source used to illuminate the entrance slits. 
However, for various practical reasons (like time and money) this was not possible, and UVIS was launched before the flatfield correction was properly determined. 
Therefore, UVIS is limited to using astrophysical sources to derive the flatfield correction. 
Unfortunately, astrophysical sources are rarely spatially uniform (the local interstellar medium/interplanetary medium being a possible exception), and the EUV/FUV spectra of such objects (in physical units) are not as
well determined as one might like them to be.

## Spica Flatfields

Assuming that the background count rate of an instrument (from RTGs, dark counts, etc.) is low compared to the signal count rate, a star bright in the UV can serve as a good approximation to a spatially uniform source. 
The star, Spica, is relatively bright in the EUV/FUV.
Three sets of Spica observations were obtained by UVIS on 3 April 2001, 17 July 2002, and 19 May 2003.

### Row-to-Row Variations in Detector Sensitivity

Since the absolute radiometric sensitivity of the instrument has already been measured in the lab (albeit in a one-dimensional form), it is only necessary to derive the relative row-to-row, column-to-column or pixel-to-pixel variations in detector sensitivity, and then normalize this relative correction so that the absolute radiometric calibration of the instrument remains unchanged. 
This greatly simplifies the process of deriving a flatfield correction from an astrophysical source, since it is no longer critical to know the spectrum of the source object.

The flatfield correction is given by:

```{math}
F_\lambda = \frac{C_{i,m}}{A_\lambda f_i t}\frac{photons}{cm^2s}
```

where 
* F$_\lambda$ is the flux from the star at a wavelength of $\lambda$, 
* C$_{i,m}$ is the counts observed in a pixel in column _i_ on scan _m_, (i.e. a spectrum shifted 0.2 x milliradians)
* A$_\lambda$ is the effective area of a pixel illuminated with light of wavelength $\lambda$, as determined by the
laboratory calibration; and 
* f$_i$ is the flatfield correction for the pixel in column _i_.

By rotating the Cassini spacecraft about the X axis, the elevation angle of Spica changes, i.e. it appears to move along the spatial dimension of the detector. 
If the rotation of the spacecraft is held at a constant angular velocity, than the star will spend an equal amount of time in each row of the detector. 
By starting the observation with the star outside of the UVIS field of view, scanning it uniformly across the slit, and ending the observation with the star outside the instrument’s field of view on the opposite side, each row will have received equal illumination by both the star the scattered light profile associated with the star (assuming that the instrument scattering function is reasonably constant over the length of the entrance slits).

Spica is relatively bright in the EUV/FUV, so photon counting statistics are by far the largest source of noise. 
With the integration times used in the Spica observations, the total signal to noise ratio is ~30 for pixels in the EUV detector below 900A and more than an order of magnitude higher than that for all other pixels. 
The “signal” from Spica below 900A—a significant portion of it is internally-scattered light from longer wavelengths—is ~10 times greater than the count rate produced by the mesa background feature. 
Since each row of the detector has received equal illumination from the source and noise in the data is small, any difference in the counts measured in the pixels of a given column must be the result of row-to-row variations in detector sensitivity.

Dividing the average value of pixels in a particular column by the value of an individual pixel in that column yields a relative correction factor for that pixel. 
This procedure is described by the following equation:

```{math}
f_{i,j}=\frac{\sum^{60}_{j=3}C_{i,j}}{58C_{i,j}}
```

where
* f$_{i,j}$ is the flatfield correction for a pixel in column i, row j, and 
* C$_{i,j}$ is the number of counts in the pixel located in column i, row j. 

The limits of the sum are chosen such that the first few rows on either end of the detector (which are either completely or partially masked out) are excluded. 
When applied to all pixels of the detector, Eq. A.2 yields a two-dimensional flatfield correction. 
However, this flatfield only corrects for row-to-row variations in detector sensitivity. 
This means that if the detector were illuminated with a spatially-uniform, monochromatic source, all the pixels in a given column would have the same value (within photon counting statistics) after multiplying the raw data by
the flatfield correction described above. 
However, pixels in a neighboring column (or any other column on the detector, for that matter) might have a different value, even though they received the same illumination.

### Column-to-Column Varations in Detector Sensitivity

In order to obtain a correction for the column-to-column variations, it is reasonable to imagine that the spacecraft might be rotated about the Z axis, moving Spica in the dispersion direction on the detector. 
However, since Spica is a point source, only a single detector row will be illuminated. 
The trick is to start by scanning the star uniformly through the field of view by rotating about the spacecraft X axis, as described above. 
After each scan, the spacecraft is rotated slightly about the Z axis and a new scan across length of the slit—in the opposite direction to the previous scan—is begun.

Since the spacecraft was rotated by a small angle between each scan, the stellar spectra from successive scans will be shifted slightly (in the spectral dimension) relative to the previous spectra. 
If the rotation between scans is an integer multiple of the angular width of the detector pixels, pixel x in observation a will have received

```{math}
F_{i,0}=F_{i+\delta,1}=F_{i+2\delta,2}=\cdots = F_{i+m\delta,m}
```

where F$_{i,m}$ is the flux of photons incident on column i on scan m.

For the UVIS observations of Spica, the azimuth angle of the spacecraft was incremented 0.2 milliradians after each scan across the slit, resulting in a shift to the spectrum of 0.8 pixels (in the dispersion direction) relative to the previous scan.
The subpixel shift in the spectrum between successive scans means that Eq. A.3 is only strictly valid for shifts that are an integer multiple of 5. For the May 2003 observation of Spica, there were 13 scans across
the slit, with a 0.2 milliradian shift between each scan. 
Therefore, the following set of equations applies:

```{math}
F_{i,0} = F_{i+4,5} = F_{i+8,10}
F_{i,1} = F_{i+4,6} = F_{i+8,11}
F_{i,2} = F_{i+4,7} = F_{i+8,12}
F_{i,3} = F_{i+4,8} = F_{i+8,13}
F_{i,4} = F_{i+4,9}
```

So for any column on the detector, the column 4 columns away received the
same illumination 5 scans later, and the column 8 columns away received the same
illumination 10 scans later. These three values could be averaged together and the
result divided by the individual pixel values to obtain corrections for the sensitivity
of column i relative to the sensitivity of columns i+4 and i+8. There are four sets
of these identically illuminated triplets with one additional pair. Using all five sets
results in five correction factors for the sensitivity of a given column relative to its
neighbors. To decrease the statistical error in the correction factor for a given pixel, the
five values could be averaged together. This procedure, applied to all columns on the
detector produces a flatfield correction that compensates for the variations in detector
sensitivity from column to column.

Although this procedure works reasonably well for the EUV channel, where the 8-
milliradian-wide occultation slit could be used, it fails for the FUV channel, where, owing
to the presence MgF 2 lens and its support structure in the center of the occultation slit,
the lo-resolution slit was used. Since the FUV lo-resolution slit is only 1.5 milliradians
wide, Spica will be in the field of view on, at most, 7 scans. A slight twist in the slit
further reduces the number of usable scans to 5. Therefore, only the first two columns
of Eq. A.7 are applicable. Since each pixel is compared with only one other pixel on the
detector, this method is quite susceptible to errors.

By making the assumption that the flux of photons varies slowly over the range in
wavelength covered by one pixel, it is possible to use all scans where the target (Spica) is
within the UVIS field of view. The UVIS EUV channel has a spectral resolution of 2.25A
(2.75A FUV) FWHM (full width at half-maximum) and a dispersion of 0.6049A/pixel
(0.7794A/pixel FUV); more than 3 pixels fit into the width of a spectral resolution
element. Since the UVIS instruments are oversampled in the spectral dimension, the
above assumption is valid. W ith this assumption, the following set of equations now
holds:

```{math}
F_{i,m}A_\lambda t = \frac{1.0C_{i,m}}{f_i}
F_{i,m}A_\lambda t = \frac{0.2C_{i,1}}{f_i} + \frac{0.8C_{i+1,m+1}}{f_{i+1}}
F_{i,m}A_\lambda t = \frac{0.4C_{i+1,2}}{f_{i+1}} + \frac{0.6C_{i+2,m+2}}{f_{i+2}}
F_{i,m}A_\lambda t = \frac{0.6C_{i+2,3}}{f_{i+2}} + \frac{0.4C_{i+3,m+3}}{f_{i+3}}
F_{i,m}A_\lambda t = \frac{0.8C_{i+3,4}}{f_{i+3}} + \frac{0.2C_{i+4,m+4}}{f_{i+4}}
```

To see how equations A.9-A.13 are derived, we refer to Table A.l and Eq. A.I.

The top half of Table A .l shows a schematic representation of 5 pixels lying in the same
row on the detector. For each pixel, there is a flatfield correction, f,, that will be derived.
The number of counts observed in the pixel in column i on scan m is given by Q jTO.
Each pixel is divided into 5 equal subpixel regions. The lower half of Table A .l shows
schematically the illumination each pixel is receiving on each of 5 scans. The spectrum
of Spica is given as F^, and it is assumed that the spectrum is constant over the width
of one pixel (AA). On scan 0, each pixel is fully illuminated by a single spectral element
e.g. column i is completely illuminated by F^. Eq. A.9 is derived from this information
and Eq. A .l. On scan 1, the position of Spica on the detector has been displaced by 0.2
milliradians in the dispersion direction relative to its position on scan 0. As a result,
only 1/5 of F A now falls on the pixel in column i, with the remaining 4/5 falling on
the pixel in column i+1. information about the location of the spectral element F a can
again be used in conjunction with Eq.A.l to derive Eq. A.10, and so on, until all five
equations have been derived.

Equations A.9-A.13 form a system of 6 unknowns (Fa, b, b+i, fi+2, fj+3, fi+4)
in 5 equations. In order to solve this system, it is necessary to supply an additional
equation. This equation is obtained by assuming that the average row-to-row flatfield
correction has a value of 1. As the number of points included in the row-to-row calculation increases, the validity of this assumption increases. The reason for this is that
the average flatfield correction, when the entire detector is considered, must be equal
to 1. If the average flatfield correction over the whole detector were not equal to 1, this
would have the effect of modifying the laboratory calibration. This assumption yields
a final equation:

```{math}
\frac{f_i+f_{i+1}+f_{i+2}+f_{i+3}+f_{i+4}}{5}=1
```

which can be used to close the system and solve for the various flatfield corrections. This
technique can be readily extended to an include an arbitrary number of vertical scans.
For each point on the detector, m flatfield correction factors are produced, where m is
the number of scans. These are then averaged together to produce a better estimate of
the “true” column-to-column flatfield correction.
