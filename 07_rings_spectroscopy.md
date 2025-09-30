---
short_title: Rings Spectroscopy
author: E. Todd Bradley
---
(sec:rings_spec)=
# Rings Spectroscopy Data Reduction

```{admonition} Conversion status: Raw
Layout unfinished and no figures yet
```

## Introduction <!-- 7.1 -->

This document describes an approach for using the Cassini UVIS spectra for analysis of
Saturn’s rings. Observations of Saturn’s rings with the UVIS began at orbit insertion in 2004 and
will continue throughout the extended mission. The majority of rings spectroscopic observations
have been configured with the UVIS acting as the secondary instrument; thus the observational
geometry and spacecraft slew rate have been driven by other instruments. As of January, 2011
the UVIS had only been the primary instrument one time for making rings spectroscopic
measurements. This may not be the case for the extended mission where the UVIS may be used
as the primary instrument for ring spectroscopy. Nevertheless, as a secondary rider the UVIS has
acquired hundreds of spectroscopic observations of the rings. Observations of the rings by the
UVIS for the purpose of ring spectroscopy deals with the instrument collecting solar photons that
have irradiated Saturn’s rings and either reflected back into the instrument (lit side observations)
or have been transmitted through the rings into the instrument (unlit side observations). Typically
both EUV and FUV spectra are collected. Table 7.1 lists parameters and typical observational
aspects of the rings. For a complete description of the UVIS see Esposito et al, 2004.
Rings spectroscopic data suitable for analysis requires calibration of the raw spectra and
then subsequent data reduction that depends on both observational geometry and the needs of the
investigator using the data. There is therefore no systematic approach that can be used for all
situations. However, data reduction may be broken down into distinct categories and the
importance of each determined by the investigator. This document aims to present an overview
of the important data reduction categories with the goal of conveying an approach for applying
different data reduction steps.

Wavelength range EUV (56.3-118.2 nm) FUV (111.5-191.2 nm)
Integration time 60 – 600 seconds
Spectral slit High resolution slit (0.75 mRad) or low resolution slit
(1.5 mRad). Most pre-2007 observations are high
resolution and most 2007-2010 are low resolution slit
Spectral binning Either 1 or 2 with the majority of the observations being
a 2
Spatial binning Usually always set to 1
Lit / Unlit side observations 80% lit side
Typical pixel field of view < 4000 km

Table 7.1. Parameters and observational aspects used for ring observations from orbit insertion through 2010. With
the exception of the wavelength range, all of these parameters may be varied. The values listed in this table represent
the majority of all observations made so far.

## Calibration of raw spectra <!-- 7.2 -->


Calibration consists of first subtracting a background from the raw counts. The
background arises primarily from detector dark counts introduced by Cassini’s three radioisotope
thermoelectric generators (RTGs). There are other backgrounds that may or may not contribute
to the total raw counts; however the RTG background is internal to the spacecraft and must
always be dealt with. The other backgrounds will be discussed in the next section. We then
multiply the data by a calibration factor that includes flat fielding and converts raw spectra in
counts per integration time to radiance in kilo-Rayleights/Å, where 1 kilo-Rayleigh = 10^9
photons sec-^1 cm-^2 emitted over 4π steradians. Details of the UVIS instrument and calibration are
given in Chapters 3 and 4. Figure 7.1 shows typical radiance from the B ring on the lit side.
Lyman- α is clearly present as well as the solar continuum. This data was acquired using a
spectral binning of 2 with the low resolution slit. Software developed by the UVIS team is
publicly available that will convert raw data downloaded from the PDS to calibrated data. This
software, called Cube Generator, is described in Chapter 12.

Figure 7.1 An example of radiance from the B ring measured from the lit side of the rings. Lyman- α is clearly
present. The spectra longward of 160 nm is due to solar irradiance reflecting from the rings.

## Data reduction <!-- 7.3 -->

This section describes other data reduction steps that may be taken depending on the
observational geometry and the needs of the investigator. Most of these steps depend on
observing geometry, which may be determined using Cube Generator that is described in
Chapter 12. Investigators are strongly encouraged to look at the geometrical configuration of
observations being used for analysis. Special attention should be given to the location and size of
pixels projected onto the ring plane and the angle of the line of sight with respect to the dayside
of the planet. The importance of these provisions is explained in the following subsections.


**_7.3.1 Saturn shine_**

Solar irradiance reflected from the atmosphere of Saturn may contribute to the signal by
either reflecting off of Saturn’s rings and entering into the instrument or by entering the
instrument when the Saturn-spacecraft-boresight angle is sufficiently small, also known as off-
axis light. The magnitude of Saturn shine varies on a number of factors. Presumably the peak
Saturn shine reflected from the rings is for regions extending radially outward from local noon,
with the magnitude decreasing for both increasing ring plane radius and solar hour angles away
from local noon. Similarly off-axis light peaks for small off-axis angles on the dayside
hemisphere and decreases for both increasing off-axis angle and observations away from local
noon. Furthermore, Saturn shine that reflects off of the rings and into the instrument is spectrally
modified by the reflectance properties of Saturn’s rings whereas off-axis light presumably bears
the same spectral shape as that of Saturn’s atmosphere. An expression for the reflectance of the
rings with both cases of Saturn shine included may be written as:

:::{math}
(7.1)
:::

where Fsun is the flux from the Sun divided by π, FSat is the flux from Saturn’s atmosphere
divided by π, and a, b, and c are constants. The first term on the right is due to solar radiation
being reflected/transmitted after only interacting with the rings, the second term on the right is
due to solar radiation first reflected off of Saturn’s atmosphere and then reflecting from the rings
into the instrument, and the last term on the right is due to solar radiation reflecting from
Saturn’s atmosphere and then into the instrument. Figure 7.2 shows the radiance measured from
Saturn’s atmosphere for observations that looked directly at the atmosphere. This corresponds to
FSat given in Equation 7.1. For non-negligible Saturn shine analysis code will have to be written
to solve for the constants in Equation 1. There may be situations where Saturn shine reflected
from the rings is negligible or off-axis light is negligible; in which case the constants b and c,
respectively, will be zero.

```
I = aFSunr + bFSatr + cFSat
```
```
r = I − cFSat
aFSun + bFSat
```

Figure 7.2. Normalized radiance measured from Saturn’s atmosphere. For small off-axis angles above the dayside
this spectra may contribute to the total signal from the UVIS for rings observations. Also, for observations of the
rings near local noon, a radiance such as this may reflect from the rings and contribute to the measured radiance
from the instrument.

### Skewed field of view

The optical system of the FUV and EUV channels images an extended source to
an entrance slit and is then spectrally dispersed onto a 64 spatial X 1024 spectral detector, where
the spatial direction is co-aligned along the length of the slit. The projected size of a pixel is ~ 1
mrad in the direction along the length of the slit and 0.75 mrad or 1.5 mrad in the cross slit
direction for either the high resolution or low resolution slit, respectively. Depending on the
position and orientation of the spacecraft with respect to the ring plane, the shape of a pixel may
be either rectangular or non-rectangular when projected onto the ring plane. Furthermore, the
relative motion between the spacecraft and ring plane during an integration period results in the
projected field of view being different than the instantaneous field of view. Figure 7.3 shows the
projected field of view of a pixel at the initial, middle, and final times for a three hundred second
integration period. The pixel begins in the outer B ring and moves into the Cassini Division.
Thus the data for that pixel has contributions from both rings regions. This complicates analysis
of ring observations and has led to procedures for binning the data and interpolating to evenly
spaced grids as will be discussed in the next section.


Figure 7.3. The projected pixel begins in the outer B ring and drifts into the Cassini Division. Contributions to the
signal arise from both the outer B ring and the Cassini Division. Cube generator (Chapter 12) now returns the
coordinates of the corner of the pixel at the initial, middle, and final integration period

### Binning the data

During an observation the field of view of a pixel projected onto the ring plane is affected
by the spacecraft motion and the angle and orientation at which the line of sight intersects the
ring plane. This results in pixels that are non-uniform both in size and distribution in the ring
plane. Azimuthally binning pixels within relatively large radial bins may bias the result towards
regions within bins where there is a higher concentration of pixels. Figure 7.4 shows how pixels
may be unevenly distributed within a ten thousand km radial bin in the outer B ring, denoted by
the heavy lines. In this simple example there are two pixels that lie at the outer edge of the radial
bin with other pixels overlapping one another radially for decreasing radius. Simply averaging
the spectra from all of the pixels within the ten thousand km radial bin will weight the average
towards the outer most portion of the radial bin since there are more pixels in the outer region of
the bin than in the inner region. However, notice that there are pixels outside of the radial bin on
both sides, which allows for a technique to deal with uneven sampling of the rings. An example
is taken from Bradley et al (2010) for resampling the data into an evenly spaced grid. In
anticipation of data being azimuthally binned over some radial increment, we only consider the
radial direction when resampling the data. We divide the rings into a 100 km radial grid and for
each grid element, we select all pixels that intersect that element. The size of the pixels takes into
account the skewed pixel size as described in Section 7.3.2.

