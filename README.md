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

The command above uses the default f16_1024.ckpt file.  To use one that you've downloaded other than the default simply download the ckpt to the checpoint file (and the yaml) and use them as such:

imagenet_f16_1024
python3 main2.py -p "cash rules everything around me" -cd cpu -ckpt checkpoints/vqgan_imagenet_f16_1024.ckpt -conf checkpoints/vqgan_imagenet_f16_1024.yaml --output output_new/filename


imagenet_f16_16384
python3 main2.py -p "cash rules everything around me" -cd cpu -ckpt checkpoints/vqgan_imagenet_f16_16384.ckpt -conf checkpoints/vqgan_imagenet_f16_16384.yaml --output output_new/filename

wiki
python3 main2.py -p "cash rules everything around me" -cd cpu -ckpt checkpoints/wikiart_16384.ckpt -conf checkpoints/wikiart_16384.yaml --output output_new/filename

faceshq
python3 main2.py -p "cash rules everything around me" -cd cpu -ckpt checkpoints/faceshq.ckpt -conf checkpoints/faceshq.yaml --init-image output_new/cream_coco_2__50.png --output output_new/cream_coco_3


  
  
  
  
Readme has additional instructions for GPU users.  I may update this when I move to a GPU rig for this project.

Issues:
This works with all versions at or newer than requirements.txt if you can't get it to work and keep getting "modules missing" stuff 
  1. it's probably an issue with either python version or you got a bad rpm package.  checking version w/ python3 --version and using pip3 update helped.  Also uninstalling and reinstalling packages is needed sometimes if you got a bad one from a rogue repo or something. 
  2. try a diff ckpt file...or run the checksum.  yours may be corrupted.  
  3. the one issue i've not been able to get is some ckpt files kick out a message about missing taming-transformers modules.  It is similar to this https://github.com/nerdyrodent/VQGAN-CLIP/issues/77 but taming-transformers is already installed.
  
