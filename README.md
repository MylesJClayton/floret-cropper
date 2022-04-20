# floret-cropper
Computer vision tool for detecting and cropping wheat florets from 3D-μCT scans.  
Cropping the volumes massively reduces required stroage space to about 1/20 of the original. The smaller images can also be processed by 3D-CNNs.  

Dependencies:  
pip install itk  
pip install SimpleITK  
pip install numpy  

Instructions for use:  
Place nii.gz (compressed NIFTI) scans of a floret of wheat and scanning tube in the input folder (The script runs on all nii.gz files in the folder).  
Change the sirectory string on line 13 of FloretCropper.py to match the location you git cloned this repository to.  
run the script.  
cropped images of wheat grains are placed in the output folder. 
