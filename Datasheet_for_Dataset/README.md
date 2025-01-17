# MBW Zoo Dataset

By: [Mosam Dabhi](mailto:mdabhi@andrew.cmu.edu) `<mdabhi@andrew.cmu.edu>`, Chaoyang Wang, Tim Clifford, Laszlo Jeni, Ian Fasel, Simon Lucey

As part of making dataset collection more easy and amenable in a wildly unconstrained setup, we collect a dataset of zoo animals using smartphone grade cameras, and annotate (~2\%) of the collected frames with 2D keypoint landmarks. We call this dataset the **Multiview Bootstrapping in the wild (MBW) Zoo dataset**; what follows below is the [datasheet](https://arxiv.org/abs/1803.09010) describing this data. If you use this dataset, please acknowledge it by citing the original paper.


## Motivation

1. **For what purpose was the dataset created?** *(Was there a specific task in mind? Was there a specific gap that needed to be filled? Please provide a description.)*

    This dataset was created to generate 2D and 3D labels of articulated objects in uncon- strained settings. Such unconstrained and casually collected datasets have a wide variety of applications including entertainment, neuroscience, psychology, ethology, and many fields of medicine. Large offline labeled datasets do not exist for all but the most common articulated object categories (e.g., humans, hands, cars). Hand labeling these landmarks within a video sequence is a laborious task. Learned landmark detectors can help, but can be error-prone when trained from only a few examples. As part of contribution of this paper, we provide this dataset where 2D and 3D labels are generated in very challenging scenarios, using our approach. Note that the user is required to only provide handheld videos from 2 or more views and manual 2D keypoint labels for 15 frames per video. No camera intrinsics or extrinsics information is required to generate the labels shown in this dataset.    


1. **Who created this dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)?**
    
    This dataset was created by the corresponding author, Mosam Dabhi. At the time of creation, Mosam is a graduate student at Carnegie Mellon University (CMU) in Pittsburgh, Pennsylvania, USA.
    


1. **Who funded the creation of the dataset?** *(If there is an associated grant, please provide the name of the grantor and the grant name and number.)*

    N/A.


1. **Any other comments?**
    
    N/A.





## Composition


1. **What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)?** *(Are there multiple types of instances (e.g., movies, users, and ratings; people and interactions between them; nodes and edges)? Please provide a description.)*

    Each instance is an image of an articulated object (zoo animals, birds, and fish). Approxi- mately 2-5% of images have corresponding manual 2D landmark annotation. From here on, we use the term landmark prediction and label interchangeably for convenience. For the remaining images in the sequences, the 2D and 3D landmark labels, as well as bounding box crops labels are generated by MBW. In particular, each entity also has a confidence flag that is a boolean specifying how much reliable is the label generated by MBW.


2. **<a name="instance_information">How many instances are there in total (of each type, if appropriate)? </a>** 
    

    In total, there are **16148** instances in this dataset from **7** different object categories, coming from **2** camera views. The overall dataset statistics below reflect the above description:
    

    | Object        | Frames (#) | Joints (#) | Manual labels (%)  |                Labels from MBW                              | 
    | :---          | :---:      | :---:    | :---:                |                 :---:                                       |
    | Fish          | 1456       | 12       |  2.7                 |  <img width="100" src=../graphics/gr_available.png>         | 
    | Colobus Monkey| 392        | 16       |  5.1                 |  <img width="100" src=../graphics/gr_available_grey_bg.png> |
    | Chimpanzee    | 204        | 16       |  6.3                 |  <img width="100" src=../graphics/gr_available.png>         |
    | Tiger         | 1829       | 14       |  0.4                 |  <img width="100" src=../graphics/gr_available_grey_bg.png> |
    | Clownfish     | 910        | 6        |  2.0                   |  <img width="100" src=../graphics/gr_available.png>         |    
    | Seahorse      | 480        | 6        |  2.2                   |  <img width="100" src=../graphics/gr_available_grey_bg.png> |        
    | Turtle        | 2806       | 9       |  N/A                   |  <img width="100" src=../graphics/gr_NA.png>        |            
    

**Please note**:  We are unable to provide the stereo baseline distance (m) and stereo angle (°) since the data was captured where the cameras were continuously moving thereby changing these metrics. 




3. **<a name="instance_information_2">Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set?</a>** *(If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (e.g., geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (e.g., to cover a more diverse range of instances, because instances were withheld or unavailable).)*

    It is a sample of all videos captured casually in an unconstrained environment such as zoo. It is not intended to be representative: the data was collected randomly in the order of visit. This data was collected with the intent to show the applicability of MBW in challenging data scenarios – specifically to label articulated objects in the wild at scale.




4. **<a name="pkl_information">What data does each instance consist of?</a>** *(``Raw'' data (e.g., unprocessed text or images)or features? In either case, please provide a description.)*

    The dataset ([![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7058567.svg)](https://doi.org/10.5281/zenodo.7058567)) is divided into two directories: `annot` and `images`. As names suggest, the `annot` directory contains annotations and `images` directory consists of 2-view synchronized image frames.

    ------------------

    - The annotations are provided as a `.pkl` file. The pickle files consists of following keys:

        | Key           | Description |
        | :---          | :---     |
        | W_GT          | Manual annotation. Non-NaN values for 1-2% of data. NaN values for the rest.      |
        | W_Predictions | 2D landmark predictions (labels) generated from MBW.       | 
        | S_Pred        | 3D landmark predictions (labels) generated from MBW. The 3D reconstructions are up-to-scale.       | 
        | BBox          | Bounding box crops generated from MBW          | 
        | confidence    | Flag specifying confidence for the MBW predictions. `True` specifies high confidence. `False` specifies low confidence. This flag is generated from the uncertainty equation (Eq. 2) given in the paper.          | 


    

5. **Is there a label or target associated with each instance? If so, please provide a description.**

    As noted in the column **Labels from MBW** in the [instance information table](#instance_information), labels for each instance are associated for the categories with flag **Available**. For the rest, only initial ≈ 2% `W_GT` labels are provided, since we did not run MBW that could provide us with prediction labels. We release this dataset to set a benchmark for solving challenging 2D and 3D landmark prediction tasks for in-the-wild unconstrained video captures.
    


6. **Is any information missing from individual instances?** *(If so, please provide a description, explaining why this information is missing (e.g., because it was unavailable). This does not include intentionally removed information, but might include, e.g., redacted text.)*

    The prediction labels (`W_Predictions`, `S_Pred`, `BBox`, and `confidence`) are missing for the categories where MBW is not run as shown in column **Labels from MBW** in the [instance information table](#instance_information) above.
    


7. **Are relationships between individual instances made explicit (e.g., users' movie ratings, social network links)?** *( If so, please describe how these relationships are made explicit.)*

    Instances are unrelated.

    

8. **Are there recommended data splits (e.g., training, development/validation, testing)?** *(If so, please provide a description of these splits, explaining the rationale behind them.)*

    Since the sole purpose of this data collection was to generate labels from scratch, we expect this data to be used solely for generating labels for unlabeled data. Thus, we do not explicitly provide a training/validation/testing split; however, we recognize that people may wish to do this, or to do some form of cross-validation. We would suggest cross-validation and test split by dividing the manual labels into 80/10/10 split and pick the samples via a uniform sampling strategy.

    


9. **Are there any errors, sources of noise, or redundancies in the dataset?** *(If so, please provide a description.)*

    Since the inital 2D keypoints were manually labeled, there could be some errors in the manual annotations since they were visually localized and clicked as labels.
    
    

10. **Is the dataset self-contained, or does it link to or otherwise rely on external resources (e.g., websites, tweets, other datasets)?** *(If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (i.e., including the external resources as they existed at the time the dataset was created); c) are there any restrictions (e.g., licenses, fees) associated with any of the external resources that might apply to a future user? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.)*

    The dataset needs to be downloaded using the following DOI from Zenodo server: [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7058567.svg)](https://doi.org/10.5281/zenodo.7058567)


11. **Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals' non-public communications)?** *(If so, please provide a description.)*

    No.
    


12. **Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?** *(If so, please describe why.)*

    No.
    
13. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*

    No.
    


14. **Does the dataset identify any subpopulations (e.g., by age, gender)?** *(If so, please describe how these subpopulations are identified and provide a description of their respective distributions within the dataset.)*

    N/A.


15. **Is it possible to identify individuals (i.e., one or more natural persons), either directly or indirectly (i.e., in combination with other data) from the dataset?** *(If so, please describe how.)*

    N/A.
    

16. **Does the dataset contain data that might be considered sensitive in any way (e.g., data that reveals racial or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)?** *(If so, please provide a description.)*

    N/A.
    


17. **Any other comments?**
    
    None.





## Collection Process

1. **How was the data associated with each instance acquired?** *(Was the data directly observable (e.g., raw text, movie ratings), reported by subjects (e.g., survey responses), or indirectly inferred/derived from other data (e.g., part-of-speech tags, model-based guesses for age or language)? If data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.)*

    The data was collected casually by two smartphone cameras without any constraints: meaning no guidance or instructions were given as to how the data was collected. The intention was to mimic the data captured casually by anyone holding a smartphone grade camera. Due to this reason, the cameras were continuously moving in space changing their extrinsics with respect to each other thereby making this a dynamic setup.



1. **<a name="collect">What mechanisms or procedures were used to collect the data </a> (e.g., hardware apparatus or sensor, manual human curation, software program, software API)?** *(How were these mechanisms or procedures validated?)*
    
    We captured 2-View videos from handheld smartphone cameras. In our case, we used an iPhone 11 Pro Max and an iPhone 12 Pro Max to capture the video sequences at 30 frames-per-second (fps). We use Final Cut Pro to manually synchronize the 2-View video sequences using the audio signal and time stamps. Please note that all we require are 2-view synchronized image frames and manual annotations for 1-2% of the data. As mentioned above, we are unable to provide the stereo baseline distance and stereo angles since the data was captured where the cameras were continuously moving thereby changing these metrics.


1. **If the dataset is a sample from a larger set, what was the sampling strategy (e.g., deterministic, probabilistic with specific sampling probabilities)?**

    Please refer the answer to [question #2](#instance_information) and [question #3](#instance_information_2) in Composition.
    


1. **Who was involved in the data collection process (e.g., students, crowdworkers, contractors) and how were they compensated (e.g., how much were crowdworkers paid)?**

    The lead author was helped by Shraddha Thakkar who graciously volunteered to capture the data during their visit to a Zoo.
    


1. **Over what timeframe was the data collected?** *(Does this timeframe match the creation timeframe of the data associated with the instances (e.g., recent crawl of old news articles)?  If not, please describe the timeframe in which the data associated with the instances was created.)*

    The dataset was collected on March 19, 2022.
    


1. **Were any ethical review processes conducted (e.g., by an institutional review board)?** *(If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.)*

    No review processes were conducted with respect to the collection of this data. Manual annotation was conducted by visually localizing the joints on the objects whose accuracy was confirmed by visual inspection.
    


1. **Does the dataset relate to people?** *(If not, you may skip the remaining questions in this section.)*

    No.
    


1. **Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (e.g., websites)?**

    N/A.
    


1. **Were the individuals in question notified about the data collection?** *(If so, please describe (or show with screenshots or other information) how notice was provided, and provide a link or other access point to, or otherwise reproduce, the exact language of the notification itself.)*

    N/A.
    


1. **Did the individuals in question consent to the collection and use of their data?** *(If so, please describe (or show with screenshots or other information) how consent was requested and provided, and provide a link or other access point to, or otherwise reproduce, the exact language to which the individuals consented.)*

    N/A.
    


1. **If consent was obtained, were the consenting individuals provided with a mechanism to revoke their consent in the future or for certain uses?** *(If so, please provide a description, as well as a link or other access point to the mechanism (if appropriate).)*
    
    N/A.


1. **Has an analysis of the potential impact of the dataset and its use on data subjects (e.g., a data protection impact analysis) been conducted?** *(If so, please provide a description of this analysis, including the outcomes, as well as a link or other access point to any supporting documentation.)*
    
    No. 


1. **Any other comments?**
    
    None.





## Preprocessing/cleaning/labeling


1. **Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)?** *(If so, please provide a description. If not, you may skip the remainder of the questions in this section.)*

    We did not do any specific preprocessing or cleaning of the data except what is mentioned in [question #1](#collect) of Collection Process. Manual annotations were labeled by visually localizing the joints on the objects in the limited (1-2%) image frames.
    


1. **Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)?** *(If so, please provide a link or other access point to the "raw" data.)*

    Yes, the image frames released under the `images/` directory are sampled from the original "raw" video.


1. **Is the software used to preprocess/clean/label the instances available?** *(If so, please provide a link or other access point.)*

    Yes. We used open-source [Matplotlib library](https://matplotlib.org) to visualize and label the joints. For further details, please refer [question #1] of this section.

    

1. **Any other comments?**
    
    None.





## Uses


1. **Has the dataset been used for any tasks already?** *(If so, please provide a description.)*

    Yes, the dataset has already been used for the task of 2D and 3D landmark predictions (sparse keypoints) by **MBW**. This task specifications are discussed in detail in the MBW paper.


1. **Is there a repository that links to any or all papers or systems that use the dataset?** *(If so, please provide a link or other access point.)*

    No.


1. **<a name="no_task">What (other) tasks could the dataset be used for?</a>**

    This dataset could be used for the following computer vision tasks:
    
    1. Dense 3D reconstruction of the given articulated object categories.
    2. Scene flow and optical flow generation tasks.
    3. Detection and tracking of non-rigid objects.
    4. Novel view rendering - owing to synchronized multi-view video sequences (NeRF).
    5. Estimation of cameras in space to aid the applications of robotics, like approaches in Simulataneous Localization and Mapping (SLAM).
    
    


1. **Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?** *(For example, is there anything that a future user might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g., stereotyping, quality of service issues) or other undesirable harms (e.g., financial harms, legal risks)  If so, please provide a description. Is there anything a future user could do to mitigate these undesirable harms?)*

    No, to the best of our knowledge.
    


1. **Are there tasks for which the dataset should not be used?** *(If so, please provide a description.)*

    Please refer [question #3](#no_task) of this topic. Apart from that, our answer to this question is: No, to the best of our knowledge.


2. **Any other comments?**
    
    None.




## Distribution


1. **Will the dataset be distributed to third parties outside of the entity (e.g., company, institution, organization) on behalf of which the dataset was created?** *(If so, please provide a description.)*
    
    Yes, the dataset is freely available under `CC-BY-NC` license. 


1. **How will the dataset will be distributed (e.g., tarball  on website, API, GitHub)?** *(Does the dataset have a digital object identifier (DOI)?)*
    
    The dataset is freely distributed at [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7058567.svg)](https://doi.org/10.5281/zenodo.7058567). Yes, since the dataset is hosted on Zenodo, it will have a DOI.
    


1. **When will the dataset be distributed?**
    
    Please refer to the question above.
    


1. **Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?** *(If so, please describe this license and/or ToU, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms or ToU, as well as any fees associated with these restrictions.)*
    
    The dataset is distributed under a `CC-BY-NC` license.
    


1. **Have any third parties imposed IP-based or other restrictions on the data associated with the instances?** *(If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms, as well as any fees associated with these restrictions.)*

    No.
    


1. **Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?** *(If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any supporting documentation.)*
    
    Not to our knowledge.


1. **Any other comments?**
    
    None.





## Maintenance


1. **Who is supporting/hosting/maintaining the dataset?**

    The author (Mosam Dabhi) is maintaining and hosting the dataset information page on GitHub, while the dataset itself is hosted on Zenodo.
    


1. **How can the owner/curator/manager of the dataset be contacted (e.g., email address)?**
    
    E-mail address of the corresponding author is provided at the top of this document.


1. **Is there an erratum?** *(If so, please provide a link or other access point.)*

    Currently, no. As errors are encountered, future versions of the dataset may be released (but will be versioned). The information to access the latest version (with updated DOI) will all be provided in the same GitHub location.


1. **Will the dataset be updated (e.g., to correct labeling errors, add new instances, delete instances')?** *(If so, please describe how often, by whom, and how updates will be communicated to users (e.g., mailing list, GitHub)?)*

    Same as previous.


1. **If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances (e.g., were individuals in question told that their data would be retained for a fixed period of time and then deleted)?** *(If so, please describe these limits and explain how they will be enforced.)*
    
    No.


1. **Will older versions of the dataset continue to be supported/hosted/maintained?** *(If so, please describe how. If not, please describe how its obsolescence will be communicated to users.)*
    
    Yes; all data will be versioned.


1. **If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so?** *(If so, please provide a description. Will these contributions be validated/verified? If so, please describe how. If not, why not? Is there a process for communicating/distributing these contributions to other users? If so, please provide a description.)*
    
    Errors may be submitted via the bugtracker on github. More extensive augmentations may be accepted at the authors' discretion.


1. **Any other comments?**
    
    None.



