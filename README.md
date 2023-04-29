# Generate a SD version of a normal video


## Convert video into a .jpg sequence
ffmpeg -i video.mp4 -r 25 -qscale:v 2 -s 1920x1080 frames/frame-%05d.jpg

## Use Stable Diffusion and img2img in batch
set the correct width & height, select a fixed seed, e.g. 234719090

## Convert /jpg sequence back into video (with interpolation)
ffmpeg -y -r 25 -i stable-diffusion-webui/output/frame%05d.jpg -s  1920x1080 -b:v 12M -vcode h264_nvenv -pix_fmt yuv420p -stract -2 -filter:v minterpolate='mi_mode=mci:me_mode=bidir:mc_mode=aobmc:vsbmc=1:fps=30',deflicker output_video.mp4

### example
ffmpeg -i IMG_4338.MOV -r 25 -qscale:v 2 -s 1920x1080 frames/frame-%05d.jpg