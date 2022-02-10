# Flatfielding

```
Andrew Steffl
```
> Reproduction of {cite:t}`Steffl2005-te`, Appendix A, with permission of the author.

All instruments have their own imperfections and idiosyncracies that need to be dealt with properly in order for data to be successfully interpreted. 
The Cassini UVIS is no exception; for any rigorous analysis of the UVIS data, careful attention must be paid to the detector flatfield correction.
The following is a somewhat technical description of the techniques used to derive the flatfield corrections for the UVIS EUV and FUV detectors.
These flatfields are ultimately derived from observations of the star Spica and were used in the analysis of all data in this thesis.
Reflecting their origin, these flatfields will be referred to as the Spica flatfields. 
An independent flatfield correction for the FUV channel has been derived from observations of the local interstellar medium/interplanetary medium (Don Shemansky, private communication). 
This second flatfield correction will be referred to as the LISM flatfield.

## Definitions and Instrumental Details

The UVIS CODACON (Lawrence and McClintock, 1996) detectors are subdivided into 2$^{16}$ pixels (1024 columns in the spectral dimension by 64 rows in the spatial dimension). 
Individual UVIS pixels are not square. 
Rather, they are 100 x 25 $\mu$m (spatial by spectral) in physical size and subtend a field of view of 1 x 0.25 mrad (1 mrad = 0.001 radians).

Both the EUV and FUV channels of UVIS are equipped with a 3-position slit changer mechanism. 
The three positions are referred to as the 

* occultation slit (8 mrad wide), 
* lo-resolution slit
  * 2.0 mrad wide for the EUV channel and 1.5 mrad wide for the FUV channel, and
* the hi-resolution slit
  * 1.0 mrad wide for the EUV channel and 0.75 mrad wide for the FUV channel. 
  
The FUV occultation slit is equipped with a cylindrical MgF$_2$ lens designed to spread light from a point source perpendicular to the dispersion direction, thereby preventing the FUV detector from saturating during observations of particularly bright stars.
The presence of this lens and its support structure reduce the effective field of view to an 8x8 mrad area in the center of the slit (where the lens is transmitting) and two 11x8 mrad windows at the ends of the slit. 
As such, the FUV occultation slit is poorly suited for observations designed to determine the detector flatfield correction, and therefore, the FUV lo-resolution slit was used.

A Cartesian coordinate system has been defined for the Cassini spacecraft. 
The boresights of the UVIS EUV and FUV channels are defined as the geometric center of the CODACON detectors (spectral pixel 511.5, spatial pixel 31.5).
The UVIS boresight (and the boresights of the other remote sensing instruments) is nominally aligned to the spacecraft -Y axis, while the UVIS entrance slits are approximately parallel with the spacecraft Z axis. 
The instrument azimuth angle ($\phi$) is defined as the angle a vector makes with respect to the spacecraft Y-Z axis, measured from the Z axis. 
The spacecraft coordinate system is shown relative to the orientation of UVIS in {numref}`fig:uvis-coordinates`.

:::{figure-md} fig:uvis-coordinates
<img src="figures/fig_A1_steffl.png" alt="UVIS Coordinates relative to Spacecraft cartesian system.">

The orientation of the Cassini UVIS relative to the spacecraft Cartesian coordinate system. Figure from the Cassini UVIS Calibration Report (Bill McClintock, private communication).

:::


A review of the UVIS instrument is given by {cite:t}`Esposito2004-kr`.
In addition, the Cassini UVIS Calibration Report (Bill McClintock, private communication) is an invaluable resource for those wishing a more detailed description of the instrument.

The UVIS flatfield correction is a two-dimensional, multiplicative array applied to data during the reduction process in order to correct for spatial variations in the detector sensitivity. 
This is separate from, though closely related to, the instrument calibration which is a one-dimensional multiplicative vector used to correct for variations in the detector sensitivity as a function of wavelength. 
In principle, pixel-to-pixel variations in detector sensitivity could be corrected by using a two-dimensional calibration array.
However, for largely historical reasons, these two corrections are applied separately to UVIS data.

The source of the dual correction procedures dates back to laboratory calibration of the UVIS instrument. 
The radiometric sensitivity of the UVIS instruments was measured by illuminating a large area of the detector and comparing the flux measured by the UVIS detector to that measured by a NIST calibrated diode, or to theoretical models of the spectrum (e.g. H$_2$) used to illuminate the detector. 
During the laboratory calibration, the severity of the flatfield artifacts of the UVIS detectors (especially for the FUV channel) was not fully appreciated, and so the counts over the whole detector were summed up to increase the signal to noise ratio. 
This process yielded measurements of the detector radiometric sensitivity at a few tens of wavelengths. 
The sensitivity at wavelengths other than those directly measured was derived through linear interpolation. 
In this manner, a 1024-element multiplicative calibration correction was created.

## Methods for Obtaining Flatfield Corrections

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
Three sets of Spica observations were obtained by UVIS on 
* 2001-04-03, 
* 2002-07-17, 
* 2003-05-19.

### Row-to-Row Variations in Detector Sensitivity

Since the absolute radiometric sensitivity of the instrument has already been measured in the lab (albeit in a one-dimensional form), it is only necessary to derive the relative row-to-row, column-to-column or pixel-to-pixel variations in detector sensitivity, and then normalize this relative correction so that the absolute radiometric calibration of the instrument remains unchanged. 
This greatly simplifies the process of deriving a flatfield correction from an astrophysical source, since it is no longer critical to know the spectrum of the source object.

The flatfield correction is given by:

```{math}
:label: eq:ff-corr
F_\lambda = \frac{C_{i,m}}{A_\lambda f_i t}\frac{photons}{cm^2s}
```

where 
* F$_\lambda$ is the flux from the star at a wavelength of $\lambda$, 
* C$_{i,m}$ is the counts observed in a pixel in column _i_ on scan _m_, (i.e. a spectrum shifted by 0.2 x _m_ mrad)
* A$_\lambda$ is the effective area of a pixel illuminated with light of wavelength $\lambda$, as determined by the
laboratory calibration; and 
* f$_i$ is the flatfield correction for the pixel in column _i_.

By rotating the Cassini spacecraft about the X axis, the elevation angle of Spica changes, i.e. it appears to move along the spatial dimension of the detector. 
If the rotation of the spacecraft is held at a constant angular velocity, than the star will spend an equal amount of time in each row of the detector. 
By starting the observation with the star outside of the UVIS field of view, scanning it uniformly across the slit, and ending the observation with the star outside the instrument’s field of view on the opposite side, each row will have received equal illumination by both the star the scattered light profile associated with the star (assuming that the instrument scattering function is reasonably constant over the length of the entrance slits).

Spica is relatively bright in the EUV/FUV, so photon counting statistics are by far the largest source of noise. 
With the integration times used in the Spica observations, the total signal to noise ratio is ~30 for pixels in the EUV detector below 900 Å and more than an order of magnitude higher than that for all other pixels. 
The “signal” from Spica below 900 Å --- a significant portion of it is internally-scattered light from longer wavelengths --- is ~10 times greater than the count rate produced by the mesa background feature. 
Since each row of the detector has received equal illumination from the source and noise in the data is small, any difference in the counts measured in the pixels of a given column must be the result of row-to-row variations in detector sensitivity.

Dividing the average value of pixels in a particular column by the value of an individual pixel in that column yields a relative correction factor for that pixel. 
This procedure is described by the following equation:

```{math}
:label: eq:row2row-corr
f_{i,j}=\frac{\sum^{60}_{j=3}C_{i,j}}{58C_{i,j}}
```

where
* f$_{i,j}$ is the flatfield correction for a pixel in column i, row j, and 
* C$_{i,j}$ is the number of counts in the pixel located in column i, row j. 

The limits of the sum are chosen such that the first few rows on either end of the detector (which are either completely or partially masked out) are excluded. 
When applied to all pixels of the detector, {eq}`eq:row2row-corr` yields a two-dimensional flatfield correction.
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
:label: eq:flux-between-scans
F_{i,0}=F_{i+\delta,1}=F_{i+2\delta,2}=\cdots = F_{i+m\delta,m}
```

where F$_{i,m}$ is the flux of photons incident on column i on scan m.

For the UVIS observations of Spica, the azimuth angle of the spacecraft was incremented 0.2 milliradians after each scan across the slit, resulting in a shift to the spectrum of 0.8 pixels (in the dispersion direction) relative to the previous scan.
The subpixel shift in the spectrum between successive scans means that {eq}`eq:flux-between-scans` is only strictly valid for shifts that are an integer multiple of 5. 
For the May 2003 observation of Spica, there were 13 scans across the slit, with a 0.2 milliradian shift between each scan. 
Therefore, the following set of equations applies:

```{math}
:label: eq:Fi0
F_{i,0} = F_{i+4,5} = F_{i+8,10}
```
```{math}
:label: eq:Fi1
F_{i,1} = F_{i+4,6} = F_{i+8,11}
```
```{math}
:label: eq:Fi2
F_{i,2} = F_{i+4,7} = F_{i+8,12}
```
```{math}
:label: eq:Fi3
F_{i,3} = F_{i+4,8} = F_{i+8,13}
```
```{math}
:label: eq:Fi4
F_{i,4} = F_{i+4,9}
```

So, for any column on the detector, the column 4 columns away received the same illumination 5 scans later, and the column 8 columns away received the same illumination 10 scans later. 
These three values could be averaged together and the result divided by the individual pixel values to obtain corrections for the sensitivity of column i relative to the sensitivity of columns i+4 and i+8. 
There are four sets of these identically illuminated triplets with one additional pair. 
Using all five sets results in five correction factors for the sensitivity of a given column relative to its neighbors. 
To decrease the statistical error in the correction factor for a given pixel, the five values could be averaged together. 
This procedure, applied to all columns on the detector produces a flatfield correction that compensates for the variations in detector sensitivity from column to column.

Although this procedure works reasonably well for the EUV channel, where the 8-milliradian-wide occultation slit could be used, it fails for the FUV channel, where, owing to the presence MgF$_2$ lens and its support structure in the center of the occultation slit, the lo-resolution slit was used. 
Since the FUV lo-resolution slit is only 1.5 milliradians wide, Spica will be in the field of view on, at most, 7 scans. 
A slight twist in the slit further reduces the number of usable scans to 5. 
Therefore, only the first two columns of {eq}`eq:Fi3` are applicable. 
Since each pixel is compared with only one other pixel on the detector, this method is quite susceptible to errors.

By making the assumption that the flux of photons varies slowly over the range in wavelength covered by one pixel, it is possible to use all scans where the target (Spica) is within the UVIS field of view. 
The UVIS EUV channel has a spectral resolution of 2.25 Å (2.75 Å FUV) FWHM (full width at half-maximum) and a dispersion of 0.6049 Å/pixel (0.7794 Å/pixel FUV); more than 3 pixels fit into the width of a spectral resolution element. 
Since the UVIS instruments are oversampled in the spectral dimension, the above assumption is valid. 
With this assumption, the following set of equations now holds:

```{math}
:label: eq:A.9
F_{i,m}A_\lambda t = \frac{1.0C_{i,m}}{f_i}
```
```{math}
:label: eq:A.10
F_{i,m}A_\lambda t = \frac{0.2C_{i,1}}{f_i} + \frac{0.8C_{i+1,m+1}}{f_{i+1}}
```
```{math}
:label: eq:A.11
F_{i,m}A_\lambda t = \frac{0.4C_{i+1,2}}{f_{i+1}} + \frac{0.6C_{i+2,m+2}}{f_{i+2}}
```
```{math}
:label: eq:A.12
F_{i,m}A_\lambda t = \frac{0.6C_{i+2,3}}{f_{i+2}} + \frac{0.4C_{i+3,m+3}}{f_{i+3}}
```
```{math}
:label: eq:A.13
F_{i,m}A_\lambda t = \frac{0.8C_{i+3,4}}{f_{i+3}} + \frac{0.2C_{i+4,m+4}}{f_{i+4}}
```

To see how equations {eq}`eq:A.9`-{eq}`eq:A.13` are derived, we refer to {numref}`fig:table_A.1` and 
Eq. {eq}`eq:ff-corr`.

:::{figure-md} fig:table_A.1
<img src="figures/table_A.1.png" alt="Description of Flatfield Method">

Description of Flatfield Method
:::

The top half of {numref}`fig:table_A.1` shows a schematic representation of 5 pixels lying in the same row on the detector. 
For each pixel, there is a flatfield correction, f$_i$, that will be derived.
The number of counts observed in the pixel in column _i_ on scan _m_ is given by C$_i,m$.
Each pixel is divided into 5 equal subpixel regions. 
The lower half of {numref}`fig:table_A.1` shows schematically the illumination each pixel is receiving on each of 5 scans. 
The spectrum of Spica is given as F$_\lambda$, and it is assumed that the spectrum is constant over the width of one pixel ($\Delta\lambda$).
On scan 0, each pixel is fully illuminated by a single spectral element, e.g. column _i_ is completely illuminated by F$_\lambda$. 
Eq. {eq}`eq:A.9` is derived from this information and Eq. {eq}`eq:ff-corr`.
On scan 1, the position of Spica on the detector has been displaced by 0.2 milliradians in the dispersion direction relative to its position on scan 0. 
As a result, only 1/5 of F$_\lambda$ now falls on the pixel in column _i_, with the remaining 4/5 falling on the pixel in column _i+1_.
Information about the location of the spectral element F$_\lambda$ can
again be used in conjunction with Eq {eq}`eq:ff-corr` to derive Eq. {eq}`eq:A.10`, and so on, until all five
equations have been derived.

Equations {eq}`eq:A.9`-{eq}`eq:A.13` form a system of 6 unknowns (F$_\lambda$, f$_i$, f$_{i+1}$, f$_{i+2}$, f$_{i+3}$, f$_{i+4}$ in 5 equations. 
In order to solve this system, it is necessary to supply an additional equation. 
This equation is obtained by assuming that the average row-to-row flatfield correction has a value of 1. 
As the number of points included in the row-to-row calculation increases, the validity of this assumption increases. 
The reason for this is that the average flatfield correction, when the entire detector is considered, must be equal to 1. 
If the average flatfield correction over the whole detector were not equal to 1, this would have the effect of modifying the laboratory calibration. 
This assumption yields a final equation:

```{math}
\frac{f_i+f_{i+1}+f_{i+2}+f_{i+3}+f_{i+4}}{5}=1
```

which can be used to close the system and solve for the various flatfield corrections. 
This technique can be readily extended to an include an arbitrary number of vertical scans.
For each point on the detector, m flatfield correction factors are produced, where m is the number of scans. 
These are then averaged together to produce a better estimate of the “true” column-to-column flatfield correction.

## IDL programs

Below are several IDL programs used to create the Spica flatfields.
There is also a gzipped tar file of the required data files.

The documentation at the head of the mk_flatfield* files should explain how they should be used. 
These routines can be used to create a flatfield with arbitrary binning based on the spica raster observations of July 2002 and May 2003.

For example, to create EUV and FUV flatfield files with no binning and the bad pixels masked out with NaN's, type:

```idl
IDL> mk_flatfield,euv_flatfield,euv_flatfield_err,fuv_flatfield,fuv_flatfield_err,/badpix
```

The variables `euv_flatfield`, `euv_flatfield_err`, `fuv_flatfield`, `fuv_flatfield_err` will be identical to the data contained in the IDL save file `spica_ff_post_1-13-2004.sav` that is in the folder "steffl" on the UVIS ftp site.

`spica_ff_datafiles.tar.gz` (gzipped tar file of the required data files)
This file is about 20 MB, so it's also stored on the UVIS ftp site, if that would work better for you for download. 
The full path is: `/rescha2/cassini/steffl/spica_ff_datafiles.tar.gz`

Individual Files:
* avg2.pro — This is a modified version of the routine avg.pro found in the  GSFC IDL astronomy users library. The modification allows NaN values to be handled properly.
* avgerr.pro — IDL routine that performs averaging on arrays, handling statistical errors properly.
* diverr.pro — IDL routine to divide (or multiply) two arrays together, handling statistical errors properly.
* frebin.pro — GSFC IDL astronomy user's library routine to resize an array, similar to the built-in function REBIN
* mk_flatfield.pro — Top-level IDL routine to create Spica-derived flatfields. --calls both mk_flatfield_jul02 and 
* mk_flatfield_may03. This is the primary routine to use when creating Spica flatfields.
* mk_flatfield_jul02.pro — IDL routine to create Spica-derived flatfields using only the July 2002 Spica raster scans.
* mk_flatfield_may03.pro — IDL routine to create Spica-derived flatfields using only the May 2003 Spica raster scans.
* rowsmooth.pro — IDL routine to perform smoothing of an array by an arbitrary kernel  with an odd number of elements (e.g. [1,4,6,4,1]) on a row-by-row basis. Can also be used to interpolate over NaN values via the interpolate_nan keyword
* totalerr.pro — IDL routine similar in use to the built-in routine "total",
 but handling statistical errors properly.