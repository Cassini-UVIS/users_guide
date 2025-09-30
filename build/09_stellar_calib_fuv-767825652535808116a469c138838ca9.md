---
short_title: Stellar Calibration FUV
author: Donald E. Shemansky
---
(sec:stellar_calib_fuv)=
# Stellar Calibration of the UVIS FUV Channel

## Introduction

The UVIS fuv channel has been calibrated on an absolute scale using observations of
αVir. A model of the stellar spectrum is used in the analysis to accurately account for instrument
properties. The absolute scale is fixed by calibrating the αVir spectrum against the observations
obtained using the Copernicus and IUE ( _Cp-IUE_ ) spectrographs as benchmark references. It has
been found that the laboratory based calibration of UVIS FUV agrees with the absolute scale
established by _Cp-IUE_ in the mid wavelength range 1300 - 1500 Å. The results of the analysis
shows a variable sensitivity for UVIS fuv in the long wavelength region as a function of time in
the mission. The overall sense of the change at longer wavelengths is toward higher sensitivity as
time progresses. The magnitude of the change is an order of magnitude at 1900 Å. In the cases
where the star calibrations cover all of the spatial pixels a flatfield is established. The flatfields
calculated here are preliminary and will require corrections in a few particular locations in the
spectrum where narrow spectral features in the stellar spectrum are not accurately modeled. Only
a few of the available αVir stellar calibration sequences have been reduced with the
methodology applied here, but the full set of available observations can be reduced without a
large expenditure of effort based on the present experience. The results obtained in this chapter
indicate that the understanding of the physics of scattered solar radiation by aerosols and surface
reflection will be significantly changed through the use of the spectral sensitivity curves
provided in this report. This investigation was undertaken after finding that theoretical aerosol
scattering properties could not be reconciled with observed UVIS fuv spectra.
The calibration curves developed in this chapter differ from those described in Chapter 3
because we use here a forward modeling approach. Our analysis and data reduction use forward
modeling for the purpose of accurately accounting for the effects of the instrument point spread
function (psf). The calibration data submitted to the PDS are described in Chapter 3, and account
for temporal changes in sensitivity. Differences in the sensitivity curves presented in this chapter
and those in the PDS are caused by psf effects, differences in flatfield, and in particular locations
in the spectrum. The flatfields developed here are designed to operate on prefiltered data vectors.
Comparison of the impact of these different methodologies have not been investigated in detail,
but will be examined in the future as a means of determining limitation in accuracy of reduction
processes. The data treatment described in this chapter is designed for detailed spectral modeling
and application to the construction of image cubes from UVIS system scan observations that use
the entire slit in accumulating virtual images.
Future deeper exposures with multiple scans of αVir will be conducted once per year to
provide updated accurate flatfields. The current standard starcals are adequate for determining
the time dependent spectral sensitivity.

## Stellar model and the absolute flux reference


The αVir of model emission properties at the surface of the star have been obtained from
the detailed non-LTE (nLTE) blanketed calculations by R. Kurucz and J. Aufdenberg. The model
parameters have been determined here by testing a range of blackbody temperatures underlying
the nLTE blanket in order to fit the _Cp-IUE_ observed spectra. The LISM extinction properties
have been roughly approximated in order to provide an accurate fit to the _Cp-IUE_ spectra > 1150
Å. 
The LISM properties should be refined to provide an accurate model at shorter wavelengths.
Our nominal stellar model at the observing instrument that conforms to the _Cp-IUE_ spectra falls
within the uncertainties in visible-infrared measurements of surface temperature, stellar radius,
and distance to the star. αVir is a binary and both components are included in the present model,
although the smaller companion has only a small effect. The stellar parameters are given in Table {ref}`tab:alpha_vir`.
The Copernicus spectrum is obtained from Code et al.(1979) (see Herbison-Evans et al.,
1971; Rogerson et a., 1973; Code et al., 1970; Meade & Code, 1980), and the IUE spectrum,
swp50032rl, from M. Festou (private communication).

:::{table} Physical Properties of αVir.
:label: "tab:alpha_vir"
:align: center

| Star$^a$ | r$^b$ | r0$_\bullet^c$ | T$^d$ | v$^e$ |
|----------|-------|----------------|-------|-------|
| Primary  | 73.6  | 7.97           | 23000 | 1.    |
| Secondary| 73.6  | 3.64           | 19000 | 1.    |

$^a$ binary period 4 d; E(B-V) = 0.025

$^b$ distance (pc)

$^c$ radius in solar radii

$^d$ surface temperature (K)

$^e$ radial velocity (km s$^{-1}$)
:::

Figure 9. 1 shows the stellar model compared to the _Cp-IUE_ observations. The model
deviates from the Copernicus spectrum at and below 1100 Å, but the spectra are well-filled by
the model over the full range of the UVIS fuv. The spectra are given in absolute photon flux
units as indicated in the figure. The model spectrum, calculated at a resolution of about R
~15000, is convoluted with a 2 Å Gaussian point spread function (psf) in Figure 9. 1. The αVir
model is based on the privately communicated nLTE calculations by R. Kurucz and J.
Aufdenberg.


Figure 9 .1: Comparison of αVir spectra from Copernicus and IUE exposures giving differential photon flux in the
range 900 – 2000Å. The nLTE calculations of blanketed surface flux by R. Kurucz and J. Aufdenberg are plotted on
the observed spectra as indicated.

(sec:stellar_calib_reduc_method)=
## Reduction methodology

UVIS FUV star calibration raw data obserbed in 2003 and 2005 were obtained from G.
Holsclaw (see Chapter 3 by Holsclaw). Archived data from 2001 are from an exposure of 1740s
duration (2001 093 09 05 28) centered on spatial pixel (pxs) 32. The data from 2003 consists of
14 files (2003 139 18 12 02 - 2003 140 06 22 38) used by A. Steffl in flatfield development. The
data from 2005 is a single scan (2005 295). The scans in 2003 and 2005 were at a rate of 0.02
mrad s-^1 , giving an assumed 50s integration period per pixel. Unlike the standard approach (see
Chapter 3, section 5), no spectral data numbers are excluded in the reduction process. The author
disagrees with discarding the “evil” pixels (Chapter 3). In this alternate approach, we average
over all pixels not excluding any, resulting in a reduced spectral resolution. The normal reduction
process at Space Environment Technologies/Planetary and Space Science Division (SET/PSSD)
is to filter the spectral vectors using a single normalized 1 , 4 , 6 , 4 ,1 pass filter. This process
moderately reduces the spectral resolution, while providing a much more tractable fixed pattern
correction. This is not considered a loss of information because the fixed pattern in the fuv
channel is severe. Figure 9. 2 shows the data reduction in selected pxs (spatial pixels) for 2001,
2003, and 2005. The results shown here are counts normalized to a 100s pxs-^1 integration period.


The nLTE αVir model after transformation by the UVIS fuv instrument simulator is plotted
twice in this figure, once using the laboratory sensitivity curve (calibration file cuvisfu10.cal),
and once using the curve modified to fit the 2001 observation (cuvisfu11.cal). The model and
data show agreement to ~10% in the 1200 – 1500 A region, indicating agreement between the
independently calibrated Copernicus, IUE, and UVIS fuv in this part of the spectrum. The known
strong depletion in pxs 32 shown in the 2003 and 2005 data is evident in Figure 9. 2 , although
there is an indication of a moderate recovery in 2005. At wavelengths > 1500 Å increasing
sensitivity with time is evident. In this analysis pxs 24 is used as the calibration reference for the
2003 and 2005 data and pxs 32 for 2001 by necessity.

Figure 9.2: Comparison of αVir spectra from UVIS fuv exposures giving signal counts (100s pxs)-^1 in the range
1100 – 1900Å. The forward modeled nLTE calculations of blanketed surface flux by R. Kurucz and J. Aufdenberg
are plotted on the observed spectra using the original laboratory calibration file and the calibration file fitting the
2001 measurement. The 2001 exposure was centered on pxs 32 only. The 2003 and 2005 data for pxs 32 and 24 are
shown on the plot. In the 1200 - 1400Å region the 2003 and 2005 pxs 32 response shows severe depletion, while psx
24 is similar to 2001 pxs 32.

### Spectral sensitivity curve derivation

The UVIS fuv sensitivity curves are determined by dividing the data by the model of the
fuv spectrograph signal for αVir. The instrument sensitivity and flatfield corrections should be
handled at the same time: the instrument sensitivity will differ if anomalous pixels with less
sensitivity are deleted. In our methodology the spectrum in row 24 is chosen as the reference


vector for 2003 and 2005. The 2001 sensitivity in row 32 is apparently very close in magnitude
to the later data in row 24, so the earlier calibration based on row 32 is consistent with the later
observations. Figure 9. 3 shows the ratio of data to model for the 2001 pxs 32 exposure based on
cuvisfu10.cal, and the derived cuvisfu11.cal. The cuvisfu11.cal curve is determined by
establishing a loess fit to the data/model ratio for cuvisfu10.cal and scaling the resulting curve to
achieve a low-pass curve with a constant mean value of 1, giving cuvisfu11.cal as the best
current estimate of UVIS sensitivity.

Figure 9.3: The ratio of the UVIS fuv 2001 093 αVir exposure at row 32 to the nLTE model simulation using the
original lab calibration sensitivity curve cuvisfu10.cal, compared to the ratio obtained using the simulation with
sensitiviy curve cuvisfu11.cal. The cuvisfu11.cal curve is obtained from a low-pass loess fit to the ratio using the
simulation with cuvisfu10.cal.

The sensitivity curves derived from the data used in this analysis compared to the original
lab calibration are shown in Figure 9 .4. The sensitivity is given in count rate per kR for the low
resolution slit. The sensitivity quantity refers to a monochromatic source at a given wavelength
and therefore is not a differential quantity. The curves show very small changes with time in the
1250 – 1500 Å region. At longer wavelengths the temporal trend is consistently toward higher
sensitivity with advancing time. At 1900 Å the laboratory determined sensitivity is below the
value in 2005 by a factor of ~8.


Figure 9.4: Sensitivity of the UVIS fuv channel determined from the laboratory calibration, compared to results
from observations of αVir in 2001, 2003, and 2005. The sensitivity refers to a monochromatic source at a given
wavelength.

Figure 9. 5 gives the fundamental intrinsic sensitivity in units of counts per photon for the
UVIS fuv corresponding to the Rayleigh brightness scale given in Figure 9. 4.


Figure 9.5: Intrinsic monochromatic efficiency, ε (counts/photon), of the UVIS fuv channel determined from the
laboratory calibration, compared to results from observations of αVir in 2001, 2003, and 2005.

## Discussion

In general, the sensitivity curves should be used with the corresponding flatfield vectors
obtained using the methodology applied here, because the sensitivity varies from row to row.
Users interested in this approach should contact the author directly for the latest flat field
corrections. In Section 9.3, it was pointed out that selected data values in fuv spectral pixels
(pxw) are not removed from the analysis as they have been in standard reductions at LASP (See
Chapter 3). All pxw values are given equal weight in the current approach described in this
chapter, which is designed specifically to ensure integrity for the reduction of system scans and
emission spectral analysis. The flatfield vectors obtained with the present derivation will require
adjustment at a few specific spectral locations where artifacts result from structure in the αVir
spectrum. Future adjustments will be made using flatfields developed from LISM exposures. The
LISM flatfields will be systematically compared to the stellar reductions to ensure integrity.


