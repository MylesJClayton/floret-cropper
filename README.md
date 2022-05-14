# floret-cropper
Computer vision tool for detecting and cropping wheat florets from 3D-μCT scans.  
Cropping the volumes massively reduces required stroage space to about 1/20 of the original. The smaller images can also be processed by 3D-CNNs.  

## Dependencies:  
pip install itk  
pip install SimpleITK  
pip install numpy  

## Instructions for use:  
From virtual environment (such as anaconda) call the script from the command line with python. 
Windows example : >python FloretCropper.py -t -i C:/path/to/input/directory -o D:/path/to/output/directory 
 
Note: * When using -i and -o, A backslash is used to denote subdirectories on both Linux and Windows *




## Arguments 
```
  -h, --help            show this help message and exit
  -i INPATH, --inpath INPATH
                        Input directory absolute path
  -o OUTPATH, --outpath OUTPATH
                        Output directory absolute path
  -t, --troubleshoot    Save images of intermediate steps threshold, components, and mask
  -n, --normalize       Normalize cropped images to have zero mean and unit variance across all voxels 
```

## Methodology  
The script makes a note of each nii.gz file in the input directory and the following process is applied for each one: 
- Image is read 
- Otsu filter determines threshold based on intensity histogram, this seperates dense objects from background (scan tube and grain) 
- A binary mask of forground/background is made * 
- Objects not connected to each other are labelled from 1 to n according to size (largest is 1) * 
- 2nd largest object is assumed to be ROI (scan tube is always largest object in the image) and mask is made * 
- A bounding box of the grain is obtained and expanded to include surroundings (other floral organs) 
- Bounding box volume is extracted/cropped out and saved 
- Voxel size of plantmatter and bounding box dimensions are recorded in a .csv 
- Cropped image of wheat grain is placed in the output folder 
- If --troubleshoot -t is specified, images of (potentially error prone) intermediate steps (*) are saved
- If --normalize -n is specified, cropped images will also be normalized to have zero mean and unit variance across all inputs
	(recommended for preprocessing images for machine learning algorithms)








