### Overview

We developed a high-throughput phenotyping pipeline for assessment of juvenile stages of kelp including semi-automated image acquisition and sporophyte trait by instance segmentation. The pipeline starts with microscopic image acquisition which can be stitched to allow for imaging of larger regions. A python script can be used to account for gradual differences in the z-axis. Afterwards, these images can be stitched with an ImageJ Macro. A Python script can be used for instance segmentation of sporophytes, including trait extraction. We provide several models and the raw data, which allows for retraining. An additional model can be used to align images, when circular markers are used on the coverslips.



**Quick links**

* manuscript
* main.py
* raw data



### Schematic overview

\---- include graphical abstract ----



### Prerequisites

* CUDA v....
* Intel I5-8500 CPU with 32 GB of RAM DDR6
* 16 GB GPU (GeForce RTX 4060 Ti)
* Metamorph v7.10.2.240 (or other microscope software)
* Microscope with motorized xy stage and camera



### Imaging pipeline

1. Prepare your sporophyte sample on a coverslip or in a multi-well plate
2. Our 3D printed holder for a 6-wells plate and 24x24 cm coverslips can be used when coverslip has to be lifted between sequentially acquired images
3. Use python script (link) to adjust z-positions in the corners
4. Start journal in Metamorph (or use different microscope control software)



### Datasets

The complete database consists of 870 images of kelp seeding material with a total of 2272 instances.



Label files are setup in the following way:

Number representing class, X,Y coordinates of polygon

Number representing class, X,Y coordinates of polygon



Classes:

1 = Egg

2 = Floating\_sporophyte (OFS)

3 = Old\_sporophyte/>64 cells

4 = Marker

5 = Young\_sporophyte/<64 cells

6 = Zygote



Number of instances per class:

1 = 140

2 = 712

3 = 449

4 = 302

5 = 461

6 = 203


Models were trained on different datasets. The datasets were reclassified and not all classes were used for each model. These databases were used to train different model sizes (s, n, m and l).

1. All developmental stages (ADS)/segAll:

   1. class 0: <64 cells + >64 cells + OFS
2. Divided developmental stages (DDS)/2C:

   1. class 0: <64 cells
   2. class 1: >64 cells + OFS
3. >64 cells/WY (without young sporophytes):

   1. class 0: >64 cells + OFS
4. Alignment/Dot:

   1. class 0: Marker



Model weights can be found in Weights.



### Output

\---- example of output ----



### Overview scripts

**Python**

* Adjustment of z-positions corner
* Rename images
* Training of YOLOv11 model (train.py) --> also validation
* Inference YOLOv11 model (main.py)



**Metamorph**

* Journal for multi-well image acquisition (6 or 32 wells)



**ImageJ**

* Stitching of images



### Overview data files

* Images
* Labels
* Yamls
* 3D print design coverslip holder

