# PL-StVO #

This code contains an algorithm to compute stereo visual odometry by using both point and line segment features.

**Authors:** [Ruben Gomez-Ojeda](http://mapir.isa.uma.es/mapirwebsite/index.php/people/164-ruben-gomez)
and [David Zuñiga-Noël](http://mapir.isa.uma.es/mapirwebsite/index.php/people/270)
and [Javier Gonzalez-Jimenez](http://mapir.isa.uma.es/mapirwebsite/index.php/people/95-javier-gonzalez-jimenez)

**Related publication:** [*Robust Stereo Visual Odometry through a Probabilistic Combination of Points and Line Segments*](http://mapir.isa.uma.es/mapirwebsite/index.php/people/164-ruben-gomez)

If you use PL-StVO in your research work, please cite:

    @InProceedings{Gomez2015,
      Title                    = {Robust Stereo Visual Odometry through a Probabilistic Combination of Points and Line Segments},
      Author                   = {Gomez-Ojeda, Ruben and Gonzalez-Jimenez, Javier},
      Booktitle                = {Robotics and Automation (ICRA), 2016 IEEE International Conference on},
      Year                     = {2016},
      Publisher                = {IEEE}
    }

The provided code is published under the General Public License Version 3 (GPL v3). More information can be found in the "GPU_LICENSE.txt" also included in the repository.

Please do not hesitate to contact the authors if you have any further questions.


## 1. Prerequisites and dependencies

### OpenCV 3.x.x
It can be easily found at http://opencv.org.

### Eigen3
http://eigen.tuxfamily.org

### Boost
Installation on Ubuntu 16.04:
```
sudo apt-get install libboost-dev
```

### YAML
Installation on Ubuntu 16.04:
```
sudo apt install libyaml-cpp-dev
```

### MRPT (>=v1.9.9)
Optional: Enables the provided visualization class.

1) Only for Ubuntu 16.04 Xenial: upgrade gcc. Instructions [here](https://gist.github.com/jlblancoc/99521194aba975286c80f93e47966dc5).
2) For any Ubuntu version older than 20.04 Focal:
```
sudo add-apt-repository ppa:joseluisblancoc/mrpt
sudo apt-get update
```
3) Everyone: Install mrpt libraries:
```
sudo apt-get install libmrpt-dev
```

### Line Descriptor
We have modified the [*line_descriptor*](https://github.com/opencv/opencv_contrib/tree/master/modules/line_descriptor) module from the [OpenCV/contrib](https://github.com/opencv/opencv_contrib) library (both BSD) which is included in the *3rdparty* folder.


## 2. Configuration and generation
A CMakeLists.txt file is included to detect external dependencies and generate the project.

The project builds "imagesStVO", a customizable application where the user must introduce the inputs to the SVO algorithm, and then process the provided output.



## 3. Usage

### Datasets configuration
We employ an environment variable, *${DATASETS_DIR}*, pointing the directory that contains our datasets. Each sequence from each dataset must contain in its root folder a file named *dataset_params.yaml*, that indicates at least the camera model and the subfolders with the left and right images. We provide dataset parameters files for several datasets and cameras with the format *xxxx_params.yaml*.

### Configuration files
For running VO we can load the default parameters file or employ the *config_xxxx.yaml* files provided for every dataset.

### VO Application
Usage: ./imagesStVO <dataset_name> [options]
Options:
	-c Config file
	-o Offset (number of frames to skip in the dataset directory
	-n Number of frames to process the sequence
	-s Parameter to skip s-1 frames (default 1)

A full command would be:

./imagesStVO kitti/00 -c ../config/config_kitti.yaml -o 100 -s 2 -n 1000

where we are processing the sequence 00 from the KITTI dataset (in our dataset folders) with the custom config file, with an offset *-c* allowing to skip the first 100 images, a parameter *-s* to consider only one every 2 images, and a parameter *-n* to only consider 1000 input pairs.
