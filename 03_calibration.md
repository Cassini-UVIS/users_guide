(sec:calib)=
# UVIS Calibration

```
Greg Holsclaw
```

## Introduction

This chapter provides an overview of the UVIS EUV and FUV channel calibration and
demonstrates how to produce calibrated data products from a PDS dataset.

## Instrument overview

The optical design of UVIS is described by {cite:t}`McClintock1993-fu` and the science
investigation by Esposito et al. (2004). 
A description of the instrument is also provided in the file [CATALOG/UVISINST.CAT](https://pds-rings.seti.org/holdings/volumes/COUVIS_0xxx/COUVIS_0003/CATALOG/UVISINST.CAT) found within any UVIS data volume in the PDS. 
A brief overview of the instrument relevant to the current discussion of calibration will be presented here.
The Cassini Ultraviolet Imaging Spectrograph (UVIS) contains four separate remote sensing
subsystems integrated in a single mechanical assembly.
These subsystems are referred to as the Far Ultraviolet Spectrograph (FUV), the Extreme Ultraviolet Spectrograph (EUV), the High Speed Photometer (HSP) and the Hydrogen-Deuterium Absorption Cell (HDAC).
Table 1 contains the design parameters for each subsystem. Because the interpretations of data from the EUV and FUV channels require a well-understood calibration, the rest of this chapter will be limited to these two subsystems only.

```{table} Summary of the UltraViolet Imaging Spectrograph design specifications
:name: table-uvis-design

||FUV  | EUV | HSP | HDAC|
|--- | --- | --- | --- | --- |
|**TELESCOPE**|||||
| Focal length (mm)| 100 | 100 | 200 | 150 |
| Entrance pupil size (mm) | 20 x 20 | 20 x 20 | 133 x 38 | 25 mm Dia|
| Reflecting surface (Material) | Al + MgF2 | Boron Carbide | Al + MgF2 | MgF2 |
| **TOROIDAL GRATINGS**|||||
| Grating radii (mm) |300, 296.1 | 300, 296.8 |||
| Grating surface | Al + MgF2 | Boron Carbide |||
| Grooves/mm | 1066 | 1371 |||
| Input angle a (degrees) | 9.22 | 8.03 |||
| Out angles b (degrees) | ±2.45 | -3.63, +1.27 |||
| Dispersion (Å/mm) | 31.18 |24.20 |||
| Dispersion (Å/pixel) | 0.7794 | 0.6049 |||
| **3-POSITION SLITS**|||||
| Slit widths (microns) | 75, 150, 800 | 100, 200, 800 |||
| Dl (Å) atmosphere | 2.75, 4.8, 24.9 | 2.75, 4.8, 19.4 |||
| Field of View (mrad) |(0.75, 1.5, 8)x60 | (1, 2, 8)x59 | 6.0 (az) x 6.4 (el) | 58 Dia (FWHM) |
|**DETECTORS**|||||
|Photocathode | CsI | KBr | CsI | KBr |
|Detector window | MgF2 |none | MgF2 | MgF2 |
|Detector size (mm) | 25.6 x 6.4 | 25.6 x 6.4 | 8 mm Dia |13 mm Dia |
| Pixel format (l x q) | 1024 x 64 | 1024 x 64 |||
| Pixel size (m) | 25 x 100 | 25 x 100 |||
```

## Terminology

As presented in Chapter 2, the NASA Planetary Data System (PDS) favors the
terminology of ‘line’ and ‘band’ to describe the perpendicular dimensions of a two-dimensional
array detector. However, the terms ‘column’ and ‘row’ are more often encountered. In this
chapter, a column will refer to all the detector elements at a given wavelength center, each of
which exists at a unique spatial location. Likewise, a row refers to all detector elements at a
given spatial location, each of which exists at a unique wavelength center. Thus, ‘columns’ are
equivalent to ‘bands’ while ‘rows’ are equivalent to ‘lines’.

## Radiometric equation

```
The number of counts recorded for a pixel at column i and row j can be expressed as:
(3.1)
```
where _Lij_ is the radiance at that pixel, _At_ is the area of the telescope entrance pupil (20 × 20 mm),
_As_ is the area of the entrance slit (three slits per channel, see Table 1), _f_ is telescope focal length
(100 mm), _K_ is the number of rows illuminated by the image of a filled slit (60 for FUV, 59 for
EUV), _FFij_ is the pixel-to-pixel sensitivity variation (also known as the “flat field”, see Section
3.5), _Ti_ is the system transmission (i.e. mirror reflectance, grating efficiency, and window transmission), QE is the quantum efficiency (detected counts per incident photon), δλ i is the

spectral width of a pixel (average of 0.07794 nm for FUV, 0.0609 nm for EUV), _t_ is the
integration time (seconds), _Bij_ is any background signal present, and _Sij_ is scattered light.
The sensitivity of the instrument was measured during laboratory calibration prior to
launch. Using this instrument sensitivity, the recorded counts can be converted to geophysical
units:
(3.2)

where _Mij_ is the inverse of the sensitivity and has units of kilorayleigh count-^1 angstrom-^1 :

```
Mij = f
```
```
2
At ⋅ As ⋅ K ⋅
```
```
1
FFij ⋅ Ti ⋅ QEi ⋅δλ i ⋅ t
```

Note that the calibration matrix provided at the PDS includes the integration time, and so the
user does not need to derive count rate (as would be more typical) before applying the
calibration. Calibrated values, resulting from the multiplication of the data and the calibration
matrix, will carry units of kilorayleigh per angstrom. The derived radiance value in Eqn. 3.2 has


significance only if the entrance slit width and pixel height (spatial dimension) is filled by the
target. The dark current of the UVIS CODACON detectors is expected to be negligible.
A persistent source of background _B_ is thought to be caused by the radioisotope
thermoelectric generators (RTGs) that power the Cassini spacecraft. Figure 3.1 shows a measure
of the FUV detector background over time, calculated by finding the mean value of all pixels in
the detector area defined by columns 950 to 1015 and rows 2 to 60 extracted from routine
observations of interplanetary hydrogen. Values derived from observations using the high-
resolution and low-resolution entrance slit are shown separately. The background from the low-
resolution data is slightly, but systematically larger than the background determined from the
high-resolution data. This difference indicates a small contribution of scattered Lyman-alpha, as
the low-resolution entrance slit is twice the width of the high-resolution slit. After filtering out
extreme values (those outside +/-30% of the median), an exponential function was fit to the low-
resolution data and is shown as the solid line in the Figure 3.1. Values above the primary trend
indicate contamination by stars or planetary bodies that have entered the field of view, or due to
ring-crossing events that have been found to significantly increase the UVIS detector
background. Values below the primary trend indicate partial data loss during downlink. The
decrease in UVIS detector background is qualitatively consistent with the expected decay of

(^238) Pu within the RTGs.
Another source of background is the relatively bright signal due to solar emission at the
Lyman-α wavelength (121.6 nm) scattered by interplanetary hydrogen (IPH). Due to scattering
within the spectrograph (see section 3.5), this IPH signal is detectable across much of the FUV
detector as well as the long-wavelength end of the EUV detector. It is recommended that
background estimates be determined for each observation independently.


```
Figure 3.1 – Background count rate in the FUV detector as a function of time.
```
## Spectrometer scattered light

The scattering properties of a spectrometer will redistribute signal at any wavelength to
other positions across the detector in a predictable manner. Ideally, a monochromatic point
source would be used to characterize this point-spread function (PSF). While there is no such
source available in-flight, sunlight scattered by interplanetary hydrogen can provide an
essentially monochromatic, though spatially extended, source.
In 1999, a campaign consisting of many long-exposure observations was conducted to
measure the instrument response to illumination by the IPH. Figure 3.2 shows an average FUV
spectrum from these observations using the low-resolution entrance slit. An analytic model
defined by a Gaussian function (to characterize the central, high signal portion of the PSF) plus a
Lorentzian function (to characterize the broad, low-signal wings) is given in Equation 3.2.
Because the signal originates from an extended source, the function must be convolved with a
rectangular function representing the geometric image of the low-resolution entrance aperture.
The model given in Eqn 3.2 was fit to the data, and is shown as a dashed line in Figure 3.2. The
model coefficients from this fit are listed in Table 3.2.


```
Figure 3.2 – Average FUV spectrum of interplanetary hydrogen along with a fit to an analytic function.
```

```{math}
:label: eq-iph-model
f = \left[a_0 + a_1\cdot \exp{\left(\frac{-0.5(x-a_2)^2}{a^2_3}\right)}+\frac{a_4}{1+\frac{1}{a_5}(x-a_2)^2}\right]\otimes rect\left(\frac{x-a_2}{w}\right)
```

### Coefficients

Here are the coefficients of the model given in {eq}`eq-iph-model` after fitting to the data shown in Figure 3.2:

```{table}
:name: tab-iph-coeffs

| Coeff | Value |
| ----  | ----  |
| $a_0$ | 0.318 |

```
