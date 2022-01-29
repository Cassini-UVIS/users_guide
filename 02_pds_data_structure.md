(sec:pds-data-structure)=
# PDS Data Structure

```{admonition} Conversion status: Close to finished
Basic layouting done, figures added. Please report issues.
```

```
David Judd
```

During the Cassini spacecraft’s tour of the solar system, the Ultraviolet Imaging Spectrograph (UVIS) has observed Venus, Earth, the Jovian and Saturn systems.
The UVIS science team has delivered data to the Planetary Data System (PDS) for storage in an historical archive. 
PDS clients are able to search, retrieve and analyze this data. 
This chapter supports those users by providing a description of UVIS data and its organization within the PDS.

In PDS, an “observation” is the fundamental organizational unit of UVIS data. 
It is a set of integers representing detector counts obtained while the instrument had a particular configuration and was obtained for a particular purpose. 
A document entitled `UVISREF.CAT` is located in all UVIS data volumes at the PDS and describes the instrument in detail. 

In summary, it describes the four subsystems of the UVIS instrument: 
* the Far Ultraviolet channel (FUV), 
* the Extreme Ultraviolet channel (EUV), 
* the High Speed Photometer (HSP), and 
* the Hydrogen/Deuterium Absorption Cell (HDAC)

and how they acquire data.

The four subsystems produce two PDS data types: 

1. cubes, and 
2. time series.

The EUV and FUV channels use detectors with a 1024x64 array of pixels, which integrate over time to generate a three dimensional matrix. 
The axes of this matrix, using PDS terminology, are _line_, _band_, and _sample_. 
The _line_ dimension is the detector’s 64 pixel spatial dimension, the _band_ is the 1024 pixel spectral dimension, and the _sample_ dimension corresponds to time where each integration of the detector is arrayed in this dimension. 
A three dimensional matrix with these axes is referred to as a **PDS cube**. 
The HSP and HDAC are photometers which produce a time ordered sequence of photon counts, corresponding to a **PDS time series**.

Regardless of its PDS data structure, there are four UVIS data products: 

1. spatial-spectral image cubes,
2. images, 
3. spectra, 
4. brightness time series. 

In each sample, a cube contains both spatial and spectral information about a target, the image contains only spatial information, and a spectrum contains only spectral information. 
The time series is a sequence of samples (photon counts). 
An image is generated from a cube by summing the detector counts across the entire wavelength dimension; a spectrum is generated from a cube by summing across the entire spatial dimension. 
The brightness time series is produced by the HSP or HDAC channels. 

These data products are illustrated in the following figures:

:::{figure-md} fig:example-cube
<img src="figures/fig_2.1.*" alt="example cube">

A spatial-spectral image cube
:::


:::{figure-md} fig:example-wavelength-image
<img src="figures/fig_2.2.*" alt="image at one wavelength">

An image at one wavelength
:::

:::{figure-md} fig:example-spectra
<img src="figures/fig_2.3.*" alt="series of spectra">

A series of spectra.
:::

A brightness series from the HSP or HDAC is a time series: {ct0, ct1, ...}.
The following surface plot in {numref}`fig:example-jupiter-image` is the first sample of a UVIS EUV spatial-spectral image cube from an observation of Jupiter:


:::{figure-md} fig:example-jupiter-image
<img src="figures/fig_2.4.*" alt="series of spectra">

The first sample of a UVIS EUV spatial-spectral image cube observation of Jupiter. 
The elevated line at y=~20 is Jupiter. 
The elevated regions at Y=~15 and Y=~25 are emissions from the Io torus. 
There are 32 lines and 512 bands of data because the binning in this observation is 2 spatially and 2 spectrally.
:::

## Windows

The EUV and FUV channels can be configured to take data from sub-regions of the
1024x64 detector called windows. 
For example, if a target is expected to be visible in the central region of the detector then a window centered around the middle of the detector with an upper left corner at (0, 24) and a lower right corner at (1023, 39) with dimensions 1024x16 would capture the target and minimize irrelevant data. 
If a reduced level of resolution is possible, then the detector could be binned to further reduce the data size. Binning is the summation of adjacent pixels, for example, binning by 2 causes adjacent pairs of pixels to be added together. 
For example this [(0, 24), (1023, 39)] window could be binned by two in the band (spectral) dimension resulting in a 512x16 array of pixels.
We take as an example two additional windows defined by window1 = ([0, 10],[1023, 14], SpecBin=1, SpaBin=5) and window3 = ([0, 50],[1023, 54], SpecBin=1, SpaBin=5). 
When windowing or binning is defined on the detector, counts are arranged within the matrix in sub-matrices corresponding to the windows of the detector. 

{numref}`fig:example-windows` illustrates this windowing and binning:

:::{figure-md} fig:example-windows
<img src="figures/fig_2.5.*" alt="example windowed data">

An example of windows in the UVIS detector
:::

The image, spectrum and cube data products are represented in the PDS as cubes. 
Images are 1 x 64 x n cubes, spectra are 1024 x 1 x n cubes and spatial-spectral image cubes are 1024 x 64 x n cubes. 
The following {numref}`fig:pds-windowed-data` provides an example UVIS cube corresponding to the windowed and binned detector configuration in {numref}`fig:example-windows`:

:::{figure-md} fig:pds-windowed-data
<img src="figures/fig_2.6.*" alt="PDS data for windowed data.">

An example of PDS data corresponding to the example offered in {numref}`fig:example-windows`.
:::

Matrix elements outside the windows contain null values (-1).
Data counts are ordered in line-major ordering. 
This structural analogy between detector windows and cubes holds for spectra and images as well. 
The solar-stellar brightness series are represented as PDS Time Series objects that are, simply, a series of detector counts, each with an associated timestamp.
To this point we have seen several configurable aspects of the UVIS instrument, namely, integration time and the detector windowing and binning. 
Windows are defined by the upper left and lower right corners of the window and an associated spatial bin and spectral bin. 
These values are specified in the PDS using name/value pairs.
In PDS format, the previous example had INTEGRATION_DURATION = 1 <SECOND>, and three windows defined using their
upper left corner, lower right corner and binning:

```
UL_CORNER_SPECTRAL = (0,0,0)
UL_CORNER_SPATIAL = (10, 24, 50)
LR_SPECTRAL = (1023, 1023, 1023)
LR_SPATIAL = (14, 39, 54)
SPATIAL_BIN = (5, 1, 5)
SPECTRAL_BIN = (1, 2, 1)
```

The structure of a UVIS Cube is specified using the 

* AXIS_NAME, 
* CORE_ITEMS,
* CORE_ITEM_BYTES, and 
* CORE_ITEM_TYPE 

values. A 1024x64x10 UVIS Cube object is specified by:

```
AXIS_NAME = (BAND, LINE, SAMPLE)
CORE_ITEMS = (1024, 64, 10)
CORE_ITEM_BYTES = 2
CORE_ITEM_TYPE = MSB_UNSIGNED_INTEGER
```

A 1024x1x10 series of spectra is specified by:

```
AXIS_NAME = (BAND, LINE, SAMPLE)
CORE_ITEMS = (1024, 1, 10)
CORE_ITEM_BYTES = 2
CORE_ITEM_TYPE = MSB_UNSIGNED_INTEGER
```

Time series are specified using ROWS, COLUMNS, ROW_BYTES, and DATA_TYPE.
The following defines a 14912 element time series of 2 byte integers:

```
ROWS = 14912
COLUMNS = 1
SAMPLING_PARAMETER_NAME = TIME
SAMPLING_PARAMETER_UNIT = MILLISECOND
SAMPLING_PARAMETER_INTERVAL= 125
...
OBJECT = COLUMN
NAME = PHOTOMETER_COUNTS
DATA_TYPE = MSB_UNSIGNED_INTEGER
BYTES = 2
```

All UVIS data objects are composed of 2 byte unsigned integers, though all values are
significantly less than 2^16.
The FUV and EUV channel data are converted into geophysical units by multiplying the
matrix of raw data by a corresponding matrix of calibration coefficients. 
This calibration is continually updated by the UVIS Team, so the user may use the latest calibration data, or if preferred, use the calibration data matrix to convert model results to expected UVIS counts for comparison. 
This calibration matrix is a 2-dimensional array with the same BAND and LINE dimensions as its corresponding data object. 
The calibration matrix contains floating point values. 
The product of the data cube and the calibration cube is data whose geophysical units are
kilorayleighs per angstrom. 
The mapping between detector columns and wavelengths is specified in the PDS BAND_BIN_CENTER value where each value in the list is a wavelength associated with the corresponding detector column. 
The process used to generate calibration coefficients is described in Chapter 3 of this user’s guide. 
Because the calibration is continually updated, the calibration matrix may change with time. 
By providing the latest calibration coefficients, we allow the user to calibrate the raw data to geophysical units (alternately, users may use their own model of the target and the instrument response to compare to the raw data). See Chapter 9 for this approach. 

HSP and HDAC data in raw form have units of counts (per integration period) and are proportional to photon flux. 
There is no additional calibration defined for these data.
PDS data objects have two components, a data component and a label component. 
The label contains a set of name/value pairs, including those listed above.
The data file contains data values formatted into a PDS object. 
These components are stored as files whose names contain the extensions DAT and LBL respectively. 
UVIS data object file names have the form <channel><start_time>.LBL or <channel><start_time>.DAT. 
The LBL files contain instrument configuration, spacecraft geometry, and taxonomic information describing UVIS data within the PDS. 
Using the information within a LBL, a reader can understand the organization of data within the DAT file and extract that data into an analysis tool. 
For example, in the IDL programming language, the read_binary function can read a data Cube such as the one defined above:

```idl
r = read_binary(‘FUV2001_001_01_02.DAT’, data_type = 2,
data_dims=[1024, 64, 10])
```

which returns a 1024x64x10 array of 2 byte integers. 
Similarly, read_binary can be used to read an HSP or HDAC data file since each is organized as a one dimensional array. 
Other configuration fields within a UVIS Cube label further describe the state of the instrument. 
For example:

```
SPACECRAFT_CLOCK_START_COUNT = "1/1633050431.160"
SPACECRAFT_CLOCK_STOP_COUNT = "UNK"
START_TIME = 2009-274T00:24:32.
STOP_TIME = 2009-274T00:36:32.
TARGET_NAME = "SOLAR WIND"
OBSERVATION_ID = 112818
INTEGRATION_DURATION = 12.500 <SECOND>
COMPRESSION_TYPE = "SQRT_9"
HI_VOLTAGE_POWER_SUPPLY_STATE = ON
OCCULTATION_PORT_STATE = OPEN
SLIT_STATE = OCCULTATION
TEST_PULSE_STATE = OFF
ODC_ID = 103
DESCRIPTION = ".. ."
```

where 
* the clock start is the Cassini clock time at the end of the first sample, 
* the start time is a text string corresponding to the spacecraft clock start time, 
* the stop time is a derived value produced by multiplying the INTEGRATION_DURATION by the number of samples, 
* the target name is a value defined during operations planning, 
* the OBSERVATION_ID is a unique numerical value associated with the observation, 
* the INTEGRATION_DURATION is the time period used to generate each sample, 
* the COMPRESSION_TYPE is the algorithm used by the UVIS flight software to encode data on-board and during transmission to earth, 
* the `HI_VOLTAGE_POWER_SUPPLY_STATE` is the voltage level applied to the detector, 
* the `OCCULTATION_PORT_STATE` is a flag indicating whether the occultation port is open or closed (i.e. whether the light source is being observed through the port), 
* the SLIT_STATE describes the width of the spectrometer entrance, 
* the TEST_PULSE_STATE indicates whether the data is internally-generated, and 
* the ODC_ID is a numeric value identifying the configuration commands generated by the operations team for this observation. 

There are two DESCRIPTION fields in a label. 
The first contains a reference to additional material for understanding the instrument state. 
The second contains a one line description of the purpose of the observation which has the form “The purpose of this observation is to...”. 
The fields relevant to understanding data are spacecraft clock, target, integration, slit state and description. 

The other fields are less important and are included in the label because they are part of UVIS telemetry:

* high voltage state is always ON, 
* test pulse is always OFF, 
* ODC_ID is used exclusively in operations management, 
* the compression algorithm, although lossy, has no significant effect on
data quality, and 
* observation ID is useful only as a reference point.

The HDAC replaces INTEGRATION_DURATION with DWELL_TIME and the H_LEVEL and D_LEVEL parameters. 
The time series generated by the HDAC channel may have additional complexity. 
If all the filament voltage levels are 0 then the HDAC is in photometer mode and its output is a time series of detector counts. 
If there is a non-zero filament voltage level the detector is in modulation mode and the time series can be mapped into a table of 32 columns, each column corresponding to an HDAC filament voltage level in the order:
d1...d16, h1...h16 where d1..d16 correspond to the 16 voltage levels of the d cell and h1..h16 the same for the h cell. 
The time series can be converted to the table by mapping contiguous subsequences into the successive columns of the table. 

The length of the subsequence is equal to the dwell time parameter of the instrument configuration. 
A data product consists of a set of data taken during a single instrument configuration.
Label files contain spacecraft pointing geometry computed for the time at the end of the first integration at the center of the field of view of the instrument. 
The keywords specifying this geometry are:

```
RIGHT_ASCENSION, DECLINATION, 
SUB_SOLAR_LATITUDE, SUB_SOLAR_LONGITUDE, 
SUB_SPACECRAFT_LATITUDE, SUB_SPACECRAFT_LONGITUDE, 
PHASE_ANGLE, EMISSION_ANGLE, INCIDENCE_ANGLE, 
CENTRAL_BODY_DISTANCE, PLANET_POSITION_VECTOR,
SC_PLANET_VELOCITY_VECTOR, SC_SUN_POSITION_VECTOR,
SC_SUN_VELOCITY_VECTOR, SC_TARGET_POSITION_VECTOR,
SC_TARGET_VELOCITY_VECTOR, PLANET_CENTER_POSITION_VECTOR,
PLANET_CENTER_VELOCITY_VECTOR
```
 
Their values are in units of degrees for angles, kilometers for distances, and kilometers/second for velocities and are given in the J2000 reference frame. 
Geometry values are generated using the NAIF SPICE toolkit. 
When a geometry value cannot be computed due to a dispersed target --- such as observation of the interplanetary medium --- or insufficient ephemeris data --- such as when the target is off-center --- a value of UNK is recorded as the parameter value. 
Since the number of interplanetary hydrogen survey observations with a target of SOLAR_WIND is relatively high, the number of UNK values is also high.
Data objects are stored in files within a data volume. 
A data volume is a directory tree whose content and structure is defined by PDS. 
The UVIS data volume has a name of the form COUVIS_nnnn where CO is an acronym for Cassini Orbiter, UVIS is the instrument name, and `nnnn` is a number in a sequence of indices. 
During the Cassini mission, UVIS produced data volumes from COUVIS_0001 through COUVIS_0060. 
The top level directory contains several directories and files:

- DATA contains data objects
- CALIB contains calibration objects
- DOCUMENT contains documentation
- CATALOG contains catalogs of data products on the volume
- SOFTWARE contains software (used for documentation only)
- AAREADME.TXT describes the data volume
- ERRATA.TXT describes know errors.

The UVIS data object files are organized by date under the DATA directory. 
The CALIB directory contains files that correspond, by name, to FUV and EUV data object files. 
These calibration files contain Cube data objects, used to convert raw counts into geophysical values.
The calibration LBL files contain a description of the calibration process. 
The SOFTWARE directory contains algorithms used to generate these coefficients and are included for reference.
The INDEX directory contains a relational database table whose columns are the fields of the LBL files and which contain the label values as records in the table. 
The purpose of the INDEX.TAB file is to provide a database search capability.
Underneath the DATA directory is a sequence of directories of the form D<yyyy>_<ddd> where yyyy is a year and ddd is a day of year. 
The contents of these directories are the observations that began on the specified day, for example,
COUVIS_0002/DATA/D2001_001/FUV2001_001_01_12.LBL. 
Underneath the CALIB directory is a subdirectory of the form VERSION_n and under that is the same directory tree as is under DATA, for example:

    COUVIS_0002/CALIB/VERSION_2/D2001_001/FUV2001_001_01_12_CAL_2.LBL.

Note that as a rule the calibration file and its corresponding data object file have corresponding names. 
Examples of data and calibration labels are given in the appendices. 
A description of the calibration version is located in the SOFTWARE/CALIB directory of each PDS data volume.
Underneath the INDEX directory are two files, INDEX.LBL and INDEX.TAB. 
The INDEX.LBL file contains a schema definition for a relational database table. 
The TAB file contains a set of records corresponding to observations, one record per observation. 
One column contains the data file name and the rest correspond to the keywords in the observation label, e.g. START_TIME, TARGET_NAME, INTEGRATION_TIME, etc. 
The index table is used to search for observations matching some user-specified criteria.
Underneath the DOCUMENT directory is the UVIS.TXT file that is a more substantial version of this chapter. 
The CATALOG directory contains the files UVISINST.CAT and UVISREF.CAT that describe the instrument in detail. 
Also included there are a description of the mission, the spacecraft and the four UVIS data products. 
The SOFTWARE directory contains algorithms encoded in the IDL programming language that are used to generate calibration coefficients and geometry. 
They are included primarily for reference. 
An IDL data reader, UVIS_PDS_READ_DATA and associated documentation are also provided.
UVIS data are available from the Atmospheres and Rings nodes of the PDS. 
From PDS, users obtain observations formatted as PDS data objects. 
By reading the object’s label a user can ascertain the structure of the data and load it into an analysis tool. The label contains all UVIS state information necessary to interpret the data. 
The steps detailed in this document will make it possible for UVIS data to be a valuable scientific resource into the foreseeable future.
