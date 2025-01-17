# Multiview Bootstrapping in the wild (MBW) - Zoo Dataset <img src="https://upload.wikimedia.org/wikipedia/en/thumb/0/08/Logo_for_Conference_on_Neural_Information_Processing_Systems.svg/1200px-Logo_for_Conference_on_Neural_Information_Processing_Systems.svg.png" width=200>


### [Paper](https://arxiv.org/abs/2210.01721) | [MBW Codebase](https://github.com/mosamdabhi/MBW) | [Project page](https://multiview-bootstrapping-in-wild.github.io) <br>

### [MBW-Zoo Dataset](https://github.com/mosamdabhi/MBW-Data): [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7058567.svg)](https://doi.org/10.5281/zenodo.7058567) | [MBW pretrained models: ![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7054596.svg)](https://doi.org/10.5281/zenodo.7054596)  <br>




<p align="center">
  <img width="750" src=graphics/overview.gif>
</p>



Table of contents
=================

<!--ts-->
   * [Overview](#overview)
      * [Abstract](#abstract)
      * [MBW-Zoo dataset](#mbw-zoo-dataset)
   * [Setup](#setup)
   * [Dataset](#dataset)
      * [Collection process](#collection-process)
      * [Frames visualization](#frames-visualization)
      * [Sequences visualization](#sequences-visualization)
      * [Joint connections visualization](#joint-connections-visualization)
      * [Predicted labels visualization](#predicted-labels-visualization)
      * [Images format](#images-format)
   * [Released dataset format](#released-dataset-format)
      * [Annotations format](#annotations-format)  
      * [Images format](#images-format)
   * [Python visualization scripts](#python-visualization-scripts)
   * [Generate labels for your own capture!](#generate-labels-for-your-own-capture)
<!--te-->

Overview
============

Abstract
------------------

Labeling articulated objects in unconstrained settings have a wide variety of applications including entertainment, neuroscience, psychology, ethology, and many fields of medicine. Large offline labeled datasets do not exist for all but the most common articulated object categories (e.g., humans). With just a few annotations (representing 1-2% of the frames), we are able to produce 2D results comparable to state-of-the-art fully supervised methods, and obtain 3D reconstructions that are impossible with other existing approaches. Our Multi-view Bootstrapping in the Wild (MBW) approach demonstrates results on standard human datasets, as well as tigers, cheetahs, fish, colobus monkeys, chimpanzees, and flamingos from videos captured casually in a zoo. 

MBW-Zoo dataset
------------------

We release a challenging dataset consisting image frames of tail-end distribution categories (such as Fish, Colobus Monkeys, Chimpanzees, etc.) with their corresponding 2D, 3D, and Bounding-Box labels generated from minimal human intervention. Some of the prominent use cases of this dataset include not only sparse **2D and 3D landmark prediction**, but also dense reconstruction tasks such as **dense deformable shape reconstruction**, novel view rendering (**NeRF**), and finally this dataset could also be used for camera estimation in Simultaneous Localization and Mapping (**SLAM**) frameworks.

The data was collected by two smartphone cameras without any constraints: meaning no guidance or instructions were given as to how the data should be collected. The intention was to mimic the data captured casually by anyone holding a smartphone grade camera. Due to this reason, the cameras were continuously moving in space changing their extrinsics with respect to each other, capturing an in-the-wild dynamic scene. Thus, this dataset could be used to benchmark robust algorithms in various computer vision tasks.




Setup
============


1. Clone the repository. 
    ```
    git clone git@github.com:mosamdabhi/MBW-Data.git
    cd MBW-Data/Data
    ```
2. Download the data zip file from here: [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7058567.svg)](https://doi.org/10.5281/zenodo.7058567)
3. Place the downloaded zip file in the `MBW-Data/Data` directory and uncompress the file.
4. Create a conda environment to run the visualization scripts.
    ```
    conda env create -f environment.yml && conda activate mbw
    ```

Dataset
============

Collection process
------------------

We capture 2-View videos from handheld smartphone cameras. In our case, we used an iPhone 11 Pro Max and an iPhone 12 Pro Max to capture the video sequences. We use Final Cut Pro to manually synchronize the 2-View video sequences using the audio signal and time stamps. Please note that all we require are 2-view synchronized image frames and manual annotations for 1-2% of the data. No camera calibration (intrinsics or extrinsics) is required to run MBW. 


Frames visualization
------------------

In total, there are **16154** instances in this dataset from **7** different object categories, coming from **2** camera views.
<p align="center">
  <img width="750" src=graphics/all_instances.jpg>
</p>


Sequences visualization
------------------
Example sequences from the capture of Fish, Chimpanzee, Colobus Monkey, and Tiger categories are shown below:
<p align="center">
  <img width="750" src=graphics/data_capture_1.gif>
</p>

Joint connections visualization 
------------------
- We manually annotate 1-2% of the image frames per view. Our annotation consists of the 2D landmark keypoints. The location of landmarks is chosen to extract articulated information from the objects. Joint connection visualization is shown below.

    | Fish        | Chimpanzee | Colobus Monkey | Tiger | Clown fish | Seahorse | Turtle |
    | :---:          | :---:     | :---:     |:---:     |:---:     |:---:     |:---:     |
    | <img width="250" src=graphics/joints_fish_no_name.jpg>     | <img width="150" src=graphics/joints_chimpanzee.jpg>    | <img width="150" src=graphics/joints_colobus_monkey.jpg>    | <img width="250" src=graphics/joints_tiger.jpg>    | <img width="150" src=graphics/joints_clownfish.jpg>    | <img width="150" src=graphics/joints_seahorse.jpg>    | <img width="150" src=graphics/joints_turtle.jpg>    


Predicted labels visualization
------------------
- We visualize the predicted 2D keypoints from **MBW** for *Fish*, *Chimpanzee*, and *Colobus Monkey* below (script to visualize is provided in this repository):

<p align="center">
  <img width="750" src=graphics/predicted_labels.gif>
</p>


Released dataset format
============



The dataset ([![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7058567.svg)](https://doi.org/10.5281/zenodo.7058567)) is divided into two directories: `annot` and `images`. As names suggest, the `annot` directory contains annotations and `images` directory consists of 2-view synchronized image frames.


Annotations format
------------------

- The annotations are provided as a `.pkl` file. The pickle files consists of following keys:

    | Key           | Description |
    | :---          | :---     |
    | W_GT          | Manual annotation. Non-NaN values for 1-2% of data. NaN values for the rest.      |
    | W_Predictions | 2D landmark predictions (labels) generated from MBW.       | 
    | S_Pred        | 3D landmark predictions (labels) generated from MBW. The 3D reconstructions are up-to-scale.       | 
    | BBox          | Bounding box crops generated from MBW          | 
    | confidence    | Flag specifying confidence for the MBW predictions. `True` specifies high confidence. `False` specifies low confidence. This flag is generated from the uncertainty equation (Eq. 2) given in the paper.          | 

Images format
------------------
The images are provided in the `images` directory as `.jpg` files.


Python visualization scripts
============

The labels provided in the `.pkl` file can be visualized with the following shell script. To run the visualization, run the following:
    ```
    cd python
    ./label_visualizations.sh
    ``` 
- Above shell script accepts the following arguments which you can change according to the need:
    | Argument        | Input options | Description | 
    | :---          | :---     | :---     |
    |    dataset       | `Fish`, `Chimpanzee`, `Colobus_Monkey` | Choose the object whose labels you want to visualize. 
    |    generate_labels_type       | `2D`, `3D`, `BBox` | Choose the type of label visualization. `2D` and `BBox` overlays the 2D landmark predictions and Bounding Box crops onto the images while `3D` label visualization generates a 3D skeleton structures with moving camera viewing angles.  
    |    vis_labels_path       | `Visualizations` | Path to store label visualizations 
    |   label_color | `blue`, `red` | Landmark (keypoint) colors for visualization 
    |img_format | `.jpg`, `.png` | Image storage format 
    | visualize_only_confident | Boolean flag |  Only visualize "confident" labels, i.e. verified as correct by MV-NRSfM Eq. (2) |
    


Generate labels for your own capture!
============
Since all we need are N-view synchroized image frames and annotations for 1-2% of data, all you need to provide are 2 or more views synchronized image frames and manual annotations for 1-2% of your data. After putting these annotations and image frames in the format shown above, **MBW** is able to provide 2D, 3D, and Bounding Box labels for your data. 

The code to run **MBW** on your own data can be found here: https://github.com/mosamdabhi/MBW


### Citation
If you use our code, dataset, or models in your research, please cite with:
```

@inproceedings{dabhi2022mbw,
	title={MBW: Multi-view Bootstrapping in the Wild},
	author={Dabhi, Mosam and Wang, Chaoyang and Clifford, Tim and Jeni, Laszlo and Fasel, Ian and Lucey, Simon},
	booktitle={Thirty-sixth Conference on Neural Information Processing Systems Datasets and Benchmarks Track},
	year={2022},
	ee = {https://openreview.net/forum?id=i1bFPSw42W0},
	organization={NeurIPS}
}


@inproceedings{dabhi2021mvnrsfm,
	title={High Fidelity 3D Reconstructions with Limited Physical Views},
	author={Dabhi, Mosam and Wang, Chaoyang and Saluja, Kunal and Jeni, Laszlo and Fasel, Ian and Lucey, Simon},
	booktitle={2021 International Conference on 3D Vision (3DV)},
	year={2021},
	ee = {https://ieeexplore.ieee.org/abstract/document/9665845},
	organization={IEEE}
}

```
