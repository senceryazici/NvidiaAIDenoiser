# NVidia AI Denoiser command line tool


##linux ubuntu 

Release Highlights NVIDIA® OptiX™ 6.0.0

add NVIDIA® OptiX™ to LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/xxx/yyy/NVIDIA-OptiX-SDK-6.0.0-linux64/lib64:$LD_LIBRARY_PATH
##update blender python addon
update exe to linux add 
 os.system('./OptiXDenoiser/Denoiser -i "{0}" -o "{0}" -hdr {1} -b {2}'.format(source_name, hdr, blend))

## Usage
Command line parameters
* -i [string] : path to input image
* -o [string] : path to output image
* -a [string] : path to input albedo AOV (optional) 
* -n [string] : path to input normal AOV (optional, requires albedo AOV) 
* -b [float] : blend amount (default 0) 
* -hdr [int] : Use HDR training data (default 1)
* -maxmem [int] : Maximum memory size used by the denoiser in MB
* -h/--help : Lists command line parameters

You need to at least have an input and output for the app to run. If you also have them, you can add an albedo AOV or albedo and normal AOVs to improve the denoising. All images should be the same resolutions, not meeting this requirement will lead to unexpected results (likely a crash). 

For best results provide as many of the AOVs as possible to the denoiser. Generally the more information the denoiser has to work with the better. The denoiser also prefers images rendered with a box filter or by using FIS.

## Examples
Here is a quick example scene that uses the images that can be found in the image folder of this repository.

### Noisy image
<p align="center">
  <img src="https://github.com/DeclanRussell/NvidiaAIDenoiser/blob/master/images/RGBA.png" alt="test"/>
</p>

### Denoised output
<p align="center">
  <img src="https://github.com/DeclanRussell/NvidiaAIDenoiser/blob/master/images/RGBA_denoised.png" alt="denoise_test"/>
</p>

# Simple sequence batch script
As it has been widely requested here is a very simple batch script for denoising sequences until I have time to implement something proper into the application itself. It will do the most simple denoising without any feature AOVs. Save the following code into a file named Sequence.bat and place it into the directory where your images are saved. Running this script will denoise all files image files that match the chosen file extension in the folder. There are three parameters that you will need to edit in the script,

* FILE_EXTENSION – the file extension of your image
* PATH_TO_DENOISER – the full directory of the Denoiser.exe
* OUTPUT_PREFIX – a prefix which is prepended to the name of the image to create the output name. I.e. with the prefix denoised_ the image test.jpg will become denoised_test.jpg

```
SET FILE_EXTENSION=jpg
SET PATH_TO_DENOISER=D:\Projects\NvidiaAIDenoiser\Denoiser_v2.0
SET OUTPUT_PREFIX=denoised_

for /r %%v in (*.%FILE_EXTENSION%) do %PATH_TO_DENOISER%\Denoiser.exe -i "%%~nv.%FILE_EXTENSION%" -o "%OUTPUT_PREFIX%%%~nv.%FILE_EXTENSION%"

cmd /k
```

# Licence info
This has no licence, do whatever you want with it just don't sue me if it breaks something!
