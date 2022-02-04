# Saturn’s Aurora

```{admonition} Conversion status: Raw
Layout unfinished and no figures yet
```

```{epigraph}
How to calibrate observations from Saturn’s poles
```

```
Jacques Gustin
```

## Introduction

In a very general sense, the aurora are luminous phenomena resulting from the collision
between precipitating charged particles and the atmosphere of a planet. Following this definition,
aurora have been observed at Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune and even at a
few satellites (Io, Europa, Ganymede). Aurora have always been observed on Earth and started
to be studied in a scientific way in the 17th century. Giant steps forward have been taken since
that time, thanks to the start of the space exploration in the late fifties. Several spacecraft and
scientific instruments have been launched and have observed the aurora of the different planets,
in multiple wavelength ranges (e.g., Voyager 1 and 2, Galileo, Image, FUSE, the Hubble Space
Telescope). The Cassini-Huygens spacecraft follows these renowned missions and has provided
unique data on Saturn’s system since 2004.
In the case of Saturn, the auroral photons in the UV are produced by the interaction
between the atmosphere and magnetospheric electrons. The magnetospheric electrons
precipitating into the atmosphere undergo elastic and inelastic collisions with the H 2 molecules
of the upper atmosphere and create secondary electrons through ionizations (see for example
Grodent et al., 2001 for more details on this process). 
The FUV auroral emission is dominated by the H$_2$ Lyman ($B^1\Sigma^+_u\rightarrow \Chi^1\Sigma^+_g$) and Werner ($C^1\Pi_u\rightarrow \Chi^1\Sigma^+_g$) system bands and the Lyman
continuum in the 900- 1700 Å bandwidth. Below 1200 Å, the emission includes the higher
energetic Rydberg transitions
( _B’_^1 _Σ_^ + _u_ → _X_^1 _Σ_^ + _g_ , _D_^1 _Πu_ → _X_^1 _Σ_^ + _g_ , _B_ ”^1 _Σ_^ + _u_ → _X_^1 _Σ_^ + _g_ , and _D_ ’^1 _Πu_ → _X_^1 _Σ_^ + _g_ ) (see Figure 3 of
Gustin et al, 2004 for more details). The auroral emission also includes lines from the atomic
hydrogen Lyman series (HLy-α at 1216 Å, Hly-β at 1025 Å,...).
The aurora can be studied through UVIS spectroscopic and imaging capabilities:

_- Low-resolution spectroscopy_. The auroral emission is potentially attenuated by the
hydrocarbon layer situated near the auroral peak. The main hydrocarbon responsible for
absorption is methane (CH 4 ), which has a significant absorption cross-section shortward of 1350
Å. By comparing the observed spectra with un-attenuated H 2 spectra (obtained from a model or
from laboratory measurements), the methane column can be derived. A model of the atmosphere
(like Moses et al. 2000) is then used to relate this methane column to the pressure level and the
H 2 column overlying the auroral emission peak. The energy deposition of the precipitated
electrons can then be estimated from a stopping power table, which gives the average path length
traveled by monoenergetic electrons into H 2 , as they slow down to rest. Examples of this
procedure may be found in the following references: Gustin et al., (2004, 2009), Dols et al.,
(2000), Ajello et al., (2005). All the UVIS auroral observations to date have been obtained with
the low-resolution slit, providing spectra at ~5.5 Å FWHM. Although this resolution is high
enough to examine the effect of hydrocarbons on the auroral emission, it is too low to resolve the
individual rotational lines and provide information on the temperature of the gas.
- _Imaging_. By slewing the 1024x64 slit above a region of interest, UVIS is able to acquire
images of the polar aurora. Images can be used to study the morphology of the aurora, determine


the brightness of the different auroral features and their variations with time, or investigate the
interaction between the ionosphere, the magnetosphere and the solar wind. See for example
Grodent et al. (2003) or Clarke et al., (2005) for more details on the auroral morphology and
ionosphere/magnetosphere interactions.

## Calibration procedures

The PDS web site contains two types of UVIS files: the raw data (*.DAT, in counts) and
a calibration matrix (*_CAL.DAT). The calibrated data in kilorayleigh per angstrom are obtained
by multiplying the raw data by the calibration matrix. For the EUV data, the combination of raw
data and calibration matrix provides the final product in kilorayleigh per angstrom for all
datasets. In the FUV, special consideration is required on a case-by-case basis because of the low
response of the “evil” pixels described in Chapter 3. Indeed, the UVIS datasets may be binned in
the spectral and/or spatial dimensions onboard Cassini to reduce data volume. If the binning is
moderate (BIN<4), the raw FUV data and calibration matrix provide the final product in
kilorayleigh per angstrom. If the binning is heavier than 4, the calibration matrix automatically
produced (*_cal.DAT) is not valid and the calibration needs special requirements. This chapter
gives details on the general calibration procedure for both the EUV and FUV UVIS channels,
with an emphasis on the FUV channel calibration in the case of heavily binned data.
It should be noted that the EUV and FUV data can be calibrated by using the “cube
generator” software described in Chapter 12. Cube Generator provides both the raw and
calibrated data, as well as all the geometric parameters needed to determine the field of view of
the instrument, the distance to the planet, the solar phase angle, etc. Cube Generator may be
used to calibrate all the EUV and the moderately binned FUV data but is not appropriate for the
heavily binned datasets.

### Read the data

The UVIS data in PDS are posted at [http://pds-rings.seti.org/cassini/uvis/access.html](http://pds-rings.seti.org/cassini/uvis/access.html)
Each dataset is composed of a *.DAT files containing the data and a *.LBL file containing
important information on how the data have been obtained (See also Chapter 2). Here are the
main variables needed to read/calibrate the data in the *.LBL file for dataset
FUV2005_172_03_35.DAT:

AXIS_NAME = (BAND, LINE, SAMPLE)
CORE_ITEMS = (1024, 64, 163)
FILE_RECORDS = 163
SPACECRAFT_CLOCK_START_COUNT = "1/1498017812.897"
INTEGRATION_DURATION = 240.000 <SECOND>
SLIT_STATE = LOW_RESOLUTION
UL_CORNER_LINE = 2
UL_CORNER_BAND = 0
LR_CORNER_LINE = 61
LR_CORNER_BAND = 1023
BAND_BIN = 1
LINE_BIN = 1


In this case, 163 records (SAMPLE) of 240 seconds have been obtained, each of them
characterized by 1024 pixels in the spectra dimension (BAND) and 64 pixels in the spatial
dimension (LINE).

_Important notes_ :
a. If data compression has been performed onboard, the pixels in the spectral and/or spatial
direction are summed, although the abuse of language “rebin” is often used instead. The
keywords BAND BIN and LINE BIN give the bin performed in the spectral and spatial
directions, respectively.
b. The illuminated matrix of a given observation may be different from the [1024 x 64]
matrix of the detector. The keywords UL_CORNER_LINE, UL_CORNER_BAND,
LR_CORNER_LINE and LR_CORNER_BAND delimit the four corners of the detector
sub-array containing valid data.

To read the EUV set obtained on 2005 DOY 172 at 03:35, do:

data=read_binary(EUV2005_172_03_35.DAT',data_dims=[1024, 64,
163], endian='big', data_type=12)

For the FUV counterpart:

data=read_binary(FUV2005_172_03_35.DAT',data_dims=[1024, 64,
163], endian='big', data_type=12)

### EUV calibration 

Four aspects should be taken into account in the calibration process: the background
noise due to the RTG, the “mesa”, the flatfield, and the conversion from counts to physical units.

- RTG: The RTGs produce a constant background noise of ~4x10-^4 counts/pixel that needs
to be subtracted from the observation. If the data have been summed onboard, the RTG
background must be multiplied by LINE_BIN and BAND_BIN before subtraction.
- A small light leak allows undispersed interplanetary H Lyman-α to reach the EUV
detector for pixels <720, corresponding to wavelength shorter than 920 Å. This creates a
background referred as the “mesa” by the UVIS team. This problem is solved by having the
occultation port open during the EUV/FUV observations, which masks the leak on UVIS flight
measurements since 2007-124.
For observations obtained before this date, the data must be carefully examined to
determine if the mesa is present or not. If it is there, it should be manually subtracted from the
data using a calibration observation performed on 16 April 2007, when the telescope was pointed
on the sky. It allowed the mesa background alone to be recorded, which can be scaled and
removed from the EUV data. It should be noted that the spectral shape of the observation
background may be slightly different from the 16 April 2007 background, as the observed source
is not necessarily uniform. In that case, spectral rows that are viewing into space should be used
instead to define a background to subtract.
- For wavelengths >~1150 Å (EUV pixel 971), another wavelength dependent background
arises from internal instrument scattering of H Lyman-α. This contribution to the EUV signal is
small below 1170 Å, and is estimated to be less than 7% of the total signal, based on


comparisons with a modeled H 2 spectrum (Ajello et al., 2005). To account for this background,
the user should use a UVIS observation of the interplanetary H Lyman-α, scale it to the Lyman-
α line of the dataset under consideration and remove from the dataset the interplanetary H
Lyman-α seen in the EUV.

- When all the noise sources discussed above are subtracted from the signal, the raw
observation is ready for the next procedures. The first is the application of a flatfield. Two
flatfields are available. The first must be applied to the data for observations performed before
June 6 2002 (FLATFIELD_EUV_PREBURN) and the other one for more recent observations,
which is the case for all auroral data (FLATFIELD_EUV_POSTBURN). The flatfield (FFD)
must be first put into the size of the observation and then rebinned:
-
IDL>FFD = FFD(UL_CORNER_BAND: LR_CORNER_BAND, UL_CORNER_BAND:
LR_CORNER_LINE)
IDL>FFD = rebin(FFD,spectral dimension,spatial dimension)

For each record, FFD must then be used as a multiplier to the data matrix, previously converted
into counts seconds-^1.

- The last step of the procedure is produce the calibration curve which converts the counts
sec-^1 to kilo-Rayleigh Å-^1 and provides the wavelength scale. This is done with the
“Get_EUV_03_Lab_Calibration.pro” and “E_Flight_Wavelength.pro” procedures found at
[http://pds-rings.seti.org/volumes/COUVIS_0011/SOFTWARE/CALIB/VERSION_1/.](http://pds-rings.seti.org/volumes/COUVIS_0011/SOFTWARE/CALIB/VERSION_1/.) Four
keywords are needed before running it:
- bin_definition = [band_bin,line_bin]
- window_definition=[ul_corner_band,ul_corner_line,lr_corner_band,lr_corner_line]
- input_spectrum : selects calibration for continuous spectra (1) or for discrete lines (2).
The auroral data require input_spectrum=1
- slit_width: selects ocultation (0), low_resolution (1), or high_resolution (2) slit. To
date, all the auroral data have been collected with the low resolution slit.
- SPACECRAFT_CLOCK_START: determined by
SPACECRAFT_CLOCK_START_COUNT. In our case, SPACECRAFT_CLOCK_START
=1498017812.897

After compilation of E_Flight_Wavelength.pro and Get_EUV_03_Lab_Calibration.pro, run
Get_EUV_03_Lab_Calibration:

IDL>Get_EUV_03_Lab_Calibration,e_wavelength,e_calibration,e_cali
bration_error,slit_width,input_spectrum,window_definition,bin_de
finition,spacecraft_clock_start

The main outputs of Get_EUV_03_Lab_Calibration are:

- e_wavelength: wavelength scale associated to the spectral dimension
- e_calibration: calibration array that needs to be multiplied to the data to get the final
calibrated file.
From a calibrated file [x,y,z], a sum of rows in the x dimension produces an image, a sum
of rows y and z produces a spectrum. Figure 4.1 shows an example of EUV auroral H 2 spectrum
after calibration.


```
Figure 4.1: Example of EUV auroral H 2 spectrum after calibration (from Gustin et al., 2009)
```
### FUV calibration

The FUV channel data require several steps before analysis The following points have
been detailed in Chapter 3 and are summarized here:

- The FUV detector experienced a change in sensitivity as a function of wavelength
and time (see Chapters 3 and 9 for more details). The sensitivity is stable with time for
wavelengths ~1300 Å and below, while an increase is observed at longer wavelength. This
problem has been addressed by observing the star Spica in a regular basis and fit an exponential
function to the fractional change over time at each wavelength. A “red patch” has been included
in the FUV calibration routine (Get_FUV_07_Lab_Calibration.pro ) in order to deliver a time-
dependent calibration curve that accounts for this problem.
For data with a spectral rebin lower or equal to 2, the calibration approach described
below is exactly the same as that in Chapter 3. The data can thus be calibrated by using the
*._CAL.DAT file or Cube Generator. A significant number of pixels in the FUV detector exhibit
anomalously low responses relative to their immediate neighbors. They are called “evil pixels”
by the UVIS team. In order to eliminate the effect of these pixels, they are replaced with NaNs
(not-a-numbers) in the FUV flatflield files and can then be interpolated (see Chapter 3 ). These
NaNs may be a problem for heavily binned data because the Nan's are included in the calibration
curve in the calibration routines and as a result for data with a spectral rebin higher than 2, the
calibration curve becomes Nan for every spectral pixels and unusable. Thus a different
calibration approach than that in Chapter 3 has been taken for the heavily binned data of the
FUV observations.
- _Spectral and/or spatial rebin_ ≤ _2:_


```
The procedure is identical to the EUV pipeline:
```
- Once the data are read and converted into counts sec-^1 , the RTG background must be
subtracted to the data. This is the only background observed in the FUV channel.
- Compile F_Flight_Wavelength.pro and Get_FUV_07_Lab_Calibration.pro and run
Get_FUV_07_Lab_Calibration with slit_width, input_spectrum, window_definition and
bin_definition as previously defined. The files FLATFIELD_FUV_POSTBURN.txt and
FLATFIELD_FUV_PREBURN.txt are required in the working directory (posted at [http://pds-](http://pds-)
rings.seti.org/volumes/COUVIS_0011/SOFTWARE/CALIB/VERSION_1/):
-
IDL>Get_FUV_07_Lab_Calibration,f_wavelength,f_calibration,f_cali
bration_error,slit_width,input_spectrum,window_definition,bin_de
finition, spacecraft_clock_start

gives the wavelength scale (F_WAVELENGTH) and the conversion from counts sec-^1 to kR Å-^1
(F_CALIBRATION). Since the flatfield is already applied in the Get_FUV_07_Lab_Calibration
procedure, F_CALIBRATION contains the NaN. Once F_CALIBRATION has been applied to
the data as a multiplier, the data array needs to be interpolated to the evil pixel. This is done with
the procedure interpolate_nans2.pro.

- After compilation of interpolate_nans2, run it the following way:
-
IDL>interpolate_nans2, UVIS_kRA1, UVIS_kRA2

with UVIS_kRA1 the data before interpolation. UVIS_kRA2 is the array with the final calibrated
data.
The product obtained following the above mentioned procedure corresponds to the output
obtained from the “cube-generator”. In the case of a rebin>2, the calibration is not handled by the
“cube-generator” and the following procedure should be applied instead:

- _Spectral and/or spatial rebin > 2:_
Here the rebin of the "f_calibration" vector is altered by the large number of NaNs. This
is why the approach must be different from what is described above and in Chapter 3: the
interpolation of the calibration curve must be performed before its rebin to the size of the data.
Apply Get_FUV_07_Lab_Calibration.pro with the keywords defined in the previous
paragraph: window_definition, input_spectrum, slit_width,bin_definition= [1, line_bin]
This gives 1) F_WAVELENGTH as a 1024 vector that needs to be scaled to the spectral
dimension x of the data:

IDL> f_wavelength=rebin(f_wavelength,x)

and 2) F_CALIBRATION with 1024 pixels in the spectral dimension, with the NaNs. This
matrix must be first interpolated to the evil pixels (NaNs) and then rebinned to the dimension of
the data. It has then to be divided by the spectral rebin (the data are not rebinned in the sense of
the IDL routine, but summed by bins of the size of the spectral rebin).
After conversion of the data to counts sec-^1 and application of the RTG, the data must be
multiplied by the new F_CALIBRATION array. Since the pre-flight lab-based measurements
implicitly include the evil pixel, the interpolation of F_CALIBRATION underestimates the
sensitivity by ~10%. The data need to be multiplied by 1.10 to get the final calibrated


observations. The two plots in Figure 4.2 and Figure 4.3 show the FUV spectra from
FUV2005_172_03_35.DAT, before and after calibration respectively:

Figure 4.2: A raw spectrum of UVIS auroral observation from 2005 DOY172. In this example, all the raw spatial
pixels and records (samples) have been summed.


Figure 4.3: Same data as the observation shown in Figure 4.2 but with calibration carried out. It is seen that the
flatfield has an important effect on the pixel-to-pixel intensity distribution, while the calibration curve enhances the
two sides of the spectrum:

```
Image with all the spectral pixels summed from the
raw data:
```
```
Image with all the spectral pixels summed from the
calibrated data:
```
(^)
Figure 4.4: Same data as the observation shown in Figure 4.2 but here only the spectral pixels have been summed:
the image corresponds to the successive records put together.
This example illustrates well 1) the effect of the flatfield (vertical stripes in the left image) and 2)
the effect of the calibration curve, which enhances the long wavelength part of the spectrum (i.e.
the reflected sunlight) in the right image.


Figure 4.5: Comparison of the auroral spectrum observation in Figure 4.2 and a model that includes reflected
sunlight model and a H 2 laboratory spectrum obtained from electron impact.

The previous examples show one of the few observation where the full spectral resolution
has been preserved, providing spectra at ~5.5 Å resolution. In most of the cases, the data have
been binned by 16 or 32 in the spectral dimension. The following example shows the shape of an
auroral H 2 spectrum binned by 32. The main effect of the spectral rebin is to smooth the
spectrum and cut off a big part of the H 2 features. The procedure described in paragraph 4.3 must
be applied to get the final calibrated product.


```
Figure 4.6: An auroral H 2 spectrum binned by 32.
```
_Final note_ : The pixels at the four edges of the detectors often exhibit odd behaviors in
terms of quantum efficiency and calibration reliability (see for example the 1st and 2nd pixel in
the last example). This is why it is strongly suggested to reject these pixels in any analysis.


