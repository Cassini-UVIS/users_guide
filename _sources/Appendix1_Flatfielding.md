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

