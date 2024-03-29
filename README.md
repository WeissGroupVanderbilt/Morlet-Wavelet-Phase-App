# Morlet Wavelet Phase Application
  Version 2.0
***
This application implements the Morlet Wavelet Phase algorithm, developed primarily to measure frequency changes of Fabry Perot fringes in thin film optical reflectance spectra, 
to enable low limits of detection for optical thin film sensors. However, it can be used in any application where low noise measurement of frequency changes of an approximately 
sinusoidal signal are required. If you use this application, please cite the following paper which introduced the algorithm:

S. J. Ward, R. Layouni, S. Arshavsky-Graham, E. Segal, and S. M. Weiss, “Morlet Wavelet Filtering and Phase Analysis to Reduce the Limit of Detection for Thin Film Optical Biosensors,” ACS Sensors 6 (8),  2967-2978 (2021).

Please note that this application is for non-commercial use only.
***
## Table of Contents
### 1. Download
### 2. Installation
##### 2.1 Mac OS
##### 2.2 Windows
### 3. Running Application
##### 3.1 Settings
##### 3.2 Advanced Settings
##### 3.3 Run Analysis and Export Results
### 4. Test Data Set
### 5. Troubleshooting
### 6. FAQ
***
## 1. Download

All information to download the application is available at the website of the Weiss Group at Vanderbilt University: https://my.vanderbilt.edu/vuphotonics/resources.

To download the application, there are two options:

1.	Download an .exe file to install the application from Github at this link:
	https://github.com/WeissGroupVanderbilt/MorletWaveletPhaseApp/raw/main/Morlet%20Wavelet%20Phase%20Installer%20for%20Windows.exe
2.	Download the application as a MATLAB module from the MATLAB file exchange by searching for “Morlet Wavelet Phase”(the link is also provided on the Github page and the Weiss 
	group at Vanderbilt University website)

Select the application installer based on your operating system (Mac OS or Windows).
***
## 2. Installation

After downloading the installer, please make sure your computer is connected to the internet and then run the installer. This will install the Morlet Wavelet Phase application and 
MATLAB runtime 2021 (needed to run the application). The installation should take around 20 minutes.

###	2.1 Mac OS
For Mac users, please confirm you want to run the installer, either in the dialog box, or by going to “System preferences → Security & Privacy” and confirming at the bottom of the window. Then follow the instructions given by the installer to finish the installation process. Finally, please go to “Finder → Application→ Morlet_Wavelet_Phase” and drag the application to your application bar.
   
###	2.2 Windows
For Windows users, please ignore the firewall warning if it appears when opening the installer by pressing ‘ok’ when a dialog box pops up. Then follow the instructions given by the installer to finish the installation process.
***
## 3. Running the Application

The application will use the Morlet wavelet phase method to analyze spectral data files selected by the user. The data should be in a .txt file with two columns separated by a tab: 
the left column should contain the wavelength data and the right column should contain the corresponding intensity data. Ensure there are no headings or other text. When opening the 
application, an initializing page will show up for 5 seconds, then please wait a further 10 seconds for the application to start.
### 3.1 Settings
- Select the folder where the spectral data are stored by clicking “browse” next to the “Input folder path” field. No specific file needs to be selected during  this step. Select only the folder.
- Type in the spectral wavelength range of data that you would like the application to filter using Morlet wavelet convolution. The default range is 450nm-900nm.
- Select the desired reference file by clicking the “browse“ button next to the “Reference spectrum filename” field. The reference file must be in the same location as 
	   the “Input folder path”. The reference file should be a spectrum collected in an equilibrium state before the target molecule has been applied.
- Type in text characters that appear in the filenames of all the .txt spectrum files you would like to analyze within your selected input folder. If left blank, all .txt files will be analyzed. If the full filename is input, only that spectrum file will be analyzed.
- Select in what order you want the spectral data files to be analyzed: the options are alphanumeric (A → Z, 1 → 9) or chronologically (earliest → latest time that each spectrum file was created).
### 3.2 Advanced Settings
- Choose advanced settings (to reset parameters click “Restore Defaults”)
	- Wavelet Length: length of wavelet in wavenumber space. This parameter affects the span of spectral data points used to calculate each filtered data point. Generally 
	     it should be large enough that the edges of the wavelet have tapered to zero to avoid edge effects. Increasing the width further will marginally improve filtering with 
	     diminishing returns, but will increase computation time, and vice versa.
	- Wavenumber Interval: spacing in wavenumber for interpolated spectral data and wavelet. This can be decreased to give higher resolution which 
	     may improve results, at the expense of slowing the algorithm down, and vice versa.
	- FFT Zero Padding: zero padding at the end of the spectral data to determine resolution in frequency after an FFT has been applied. Zero padding can be increased to give a 
	     more precise estimate of the dominant frequency of the fringes, again at the expense of increased computational cost.
	- Maximum Possible Optical Thickness: specify an upper bound for the optical thickness that the thin film is guaranteed to be below. To speed up the algorithm, if the 
	     optical thickness will be below a certain value, for example 8000nm*RIU, the algorithm will not look beyond this for the dominant peak of the FFT.
	- Minimum Possible Optical Thickness: specify a lower bound for the optical thickness that the thin film is guaranteed to be above. To speed up the algorithm, if the 
	     optical thickness will be above a certain value, for example 4000nm*RIU, the algorithm will not look beyond this for the dominant peak of the FFT.
	- Wavelet Width Multiplier: width of the wavelet in frequency space. The default is to set the width of the wavelet in frequency space equal to the FWHM of the dominant 
	     peak in the FFT of the Fabry-Perot fringes, corresponding to Wavelet Width Multiplier = 1. However, this parameter can be optimized for any given system to retain maximal 
	     signal and remove maximum noise. If the fringe frequency is similar to other features in the FFT caused by noise signatures, then a narrower wavelet width in frequency 
	     space may be helpful. If the fringe frequency is well separated from the other noise contributions in the FFT then a wider wavelet width in frequency space may give better 
	     results.
	- Smaller Wavelength Process Range: if fringes are still present outside of the spectral window chosen to process the data, but these fringes are noisy, the “Spectral Range” 
	     can be widened to include these noisy fringes when filtering the data, and the Smaller Wavelength Process Range can be set to the spectral range of data with sufficiently 
	     high signal to noise ratio to carry out the final phase calculation. Filtering a larger range of data and processing a smaller slice of the filtered data may improve 
	     performance. By default, Smaller Wavelength Process Range is set from 0 – Inf, which means the entire “Spectral Range” of data is used for both filtering and processing.
### 3.3 Run Analysis and Export Results
- Click “Run Analysis”
- Once analysis is finished, the result can be exported as a .txt file or in graph form as a .jpg file by clicking the buttons “Export Results” or “Export Figure,” respectively.
***
## 4. Test Data Set

A test dataset is provided with this application both on the Weiss group website: https://my.vanderbilt.edu/vuphotonics/resources, and the Github page: 
https://weissgroupvanderbilt.github.io/MorletWaveletPhaseApp/. It consists of 491 spectrum files (named ”P00000” to “P000490”). The data was generously provided by the Segal group 
at Technion from experiments published in the following journal article:

Arshavsky-Graham, S. et al. Aptamers: Vs. Antibodies as Capture Probes in Optical Porous Silicon Biosensors. Analyst 2020, 145 (14), 4991–5003.

These spectra were collected using an immunosensor with anti-his tag antibodies immobilized in an oriented configuration. The baseline (“P00000” to “P00146”) 
and the washing steps (“P00388” to “P00490”) are in PBS buffer, while the increase in the signal corresponds to his-tagged protein target (tyrosinase) exposure at a concentration of
16.5 uM (“P00147” to “P00387”). A similar graph is shown in Figure S4B (black trace).

The resulting exported figure from the Morlet wavelet phase analysis app is also included along with the test dataset on the Weiss group website and GitHub webpage; the only non-default 
settings used were the “Maximum Possible Optical Thickness”, set to 15000, and the “Minimum Possible Optical Thickness”, set to 8000, to ensure the correct peak in the FFT is used.

***
## 5. Troubleshooting

Restart the application if it becomes unresponsive. For any other problems while installing or running the application, please contact weissgroup-code@vanderbilt.edu.
***
## 6. FAQs

***
## 7. Acknowledgements

Development of this application was funded in part by the National Institute of Health (R21AI156693).
***
