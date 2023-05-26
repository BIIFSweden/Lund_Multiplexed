# Part II - Cell segmentation and dot detection in color images.
## Overview
In this exercise we will learn how to handle colored brightfield images. Here the central part is "Color Deconvolution", where we split the colors into individual channels. We will also learn how to create a workflow script to run the workflow on a different image.

## Image data
- BJ_bf_not_stimulated.tif
- BJ_bf_stimulated.tif

## Preparations
-	Create a new project in QuPath under `File > Project`. Choose an empty folder to create the project. You can also re-use the project from part I.
-	Add the images: BJ_bf_not_stimulated.tif and BJ_bf_stimulated.tif
	
While importing set the Image type to `H-DAB`.

Let's start with `BJ_bf_not_stimulated.tif`: double-click on the image to start analysis.
The image scaling seems to be wrong. In the image tab change the pixel size to the right value (0.353 µm?).

## Color Deconvolution
Colored images come with a red, green, blue intensity value for each pixel. There are different method to digitally separate the three stains. Giving the information of `H-DAB` while importing the images to QuPath, we passed on the information of which colors we expect in the images. QuPath then automatically separates the colors into individual channels ("color deconvolution") while importing. You can read more about color deconvolution in QuPath in the documentation: https://qupath.readthedocs.io/en/0.3/docs/tutorials/separating_stains.html

Under `View > Brightness/Contrast` one can see that QuPath automatically separates the channels using different methods. Hematoxylin, DAB, Residual are the 3 resulting channels from color deconvolution, giving the information that we expect colors to follow an H-DAB color scheme.  

Let's inspect the single channels after the automatic color deconvolution: 
- Hematoxylin
- DAB
- Residual

Under `View > Brightness/Contrast` to adjust each channel. Use `show grayscale` and `invert background` to get a fluorescence-like image. We aim for seeing the signal of the blue nuclei in the Hematoxylin channel, the signal of the brown/red dots in the DAB channel. In Residual we should only see background.

With `View > Show channel viewer` you can inspect the channels in a montage view:
![](images/screenshot_channel_viewer_original.png?raw=true "Screenshot")

The automated color separation is quite good. We can still try to improve the color deconvolution. For this:
-	Draw a rectangle covering a smaller area with cells, dots and background
-	Run `Analyze > Preprocessing > Estimate stain vectors` 
-	Click `Yes` confirming the new modal RGB values as background values.  
	
![](images/screenshot_estimate_stain_vectors_bg.png?raw=true "Screenshot")
-	In the `Visual Stain Editor` we can inspect the color deconvolution. Click `Auto` to re-calculate the stain vectors according to the selected area.  
![](images/screenshot_visual_stain_editor.png?raw=true "Screenshot")
-	Click `OK` and save the settings under a new name.  
![](images/screenshot_estimate_stain_vectors.png?raw=true "Screenshot")
-	Re-inspect the single channels: Hematoxylin, DAB, Residual. 
-	![](images/screenshot_channel_viewer_adjusted.png?raw=true "Screenshot")

## Cell Detection
Once the colors are well separated to different channel, we can treat the image as any multi-channel fluorescence microscopy image data.
For cell detection we can therefore proceed as for data set 1.
- Delete the annotation used for color deconvolution and draw a rectangular annotation to cover the entire image
- Run `Analyze > Cell detection`

### Exercise: 
Try to find settings for cell detections by yourself!


<details>
	
  <summary>Suggested settings (click):</summary>
	
![](images/screenshot_settings_cell_detection.png?raw=true "Screenshot")
	
</details>

