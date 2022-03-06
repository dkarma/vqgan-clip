# VQGAN-CLIP

VQGAN-CLIP is a semantic image generation and editing methodology developed by members of EleutherAI.

This version has been tested with the included requirements file against python 3.7.  I haven't tested it with any other verison.
Photos will be generated every 50 iterations and i've changed the code so that:
1. the photo will have the iteration number (50,100,150,etc.) appended to the end of the filename ALONG WITH _.png
2. watermark.png is a 30x10 png that must sit where main2.py sits and will be applied to every pic generated.  Changing this pic size will also require the argument in main2.py to be updated:

## Quick Start
Download the zip and extract to linux folder of your choice (I use Ubuntu 16.04 flavor of linux and a sub folder in my home directory as my landing place when i extract the zip).

First install dependencies via `pip install -r requirements.txt`.

Next, download a vqgan checkpoint with a command like the curl ones below.
Checkpoints are basically large datasets that have already been trained.  Typically they are several gigs so storing multiple checkpoints / datasets will take up a lot of space!  

make a folder for them in the same folder as main2.py as an empty one isn't included:
mkdir checkpoints

curl -L -o checkpoints/vqgan_imagenet_f16_16384.yaml -C - 'https://heibox.uni-heidelberg.de/d/a7530b09fed84f80a887/files/?p=%2Fconfigs%2Fmodel.yaml&dl=1' #ImageNet 16384
curl -L -o checkpoints/vqgan_imagenet_f16_16384.ckpt -C - 'https://heibox.uni-heidelberg.de/d/a7530b09fed84f80a887/files/?p=%2Fckpts%2Flast.ckpt&dl=1' #ImageNet 16384

once these are downloaded to the checkpoints folder they can be renamed anything.ckpt and anything.yaml

additional datasets can be found here:
https://imerit.net/blog/the-60-best-free-datasets-for-machine-learning-all-pbm/

You are now ready to go! Try using one of the templates in the vqgan_commands file:
If youre testing this on a laptop like me use the -cd cpu command like this and then ignore any cuda errors that pop up when this runs.
python3 main2.py -p "wu-tang shaolin" -cd cpu --output output_new/<filename>

Readme has additional instructions for GPU users.  I may update this when I move to a GPU rig for this project.
