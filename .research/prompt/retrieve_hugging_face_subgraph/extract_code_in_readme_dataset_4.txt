
Input:
From the Hugging Face README provided in “# README,” extract and output only the Python code required for execution. Do not output any other information. In particular, if no implementation method is described, output an empty string.

# README
---
annotations_creators: []
language: en
license: other
size_categories:
- 10K<n<100K
task_categories:
- image-classification
task_ids: []
pretty_name: FGVC-Aircraft
tags:
- fiftyone
- image
- image-classification
dataset_summary: '



  ![image/png](dataset_preview.gif)



  This is a [FiftyOne](https://github.com/voxel51/fiftyone) dataset with 10000 samples.


  ## Installation


  If you haven''t already, install FiftyOne:


  ```bash

  pip install -U fiftyone

  ```


  ## Usage


  ```python

  import fiftyone as fo

  import fiftyone.utils.huggingface as fouh


  # Load the dataset

  # Note: other available arguments include ''max_samples'', etc

  dataset = fouh.load_from_hub("Voxel51/FGVC-Aircraft")


  # Launch the App

  session = fo.launch_app(dataset)

  ```

  '
---

# Dataset Card for FGVC-Aircraft

<!-- Provide a quick summary of the dataset. -->




![image/png](dataset_preview.gif)


This is a [FiftyOne](https://github.com/voxel51/fiftyone) dataset with 10000 samples.

## Installation

If you haven't already, install FiftyOne:

```bash
pip install -U fiftyone
```

## Usage

```python
import fiftyone as fo
import fiftyone.utils.huggingface as fouh

# Load the dataset
# Note: other available arguments include 'max_samples', etc
dataset = fouh.load_from_hub("Voxel51/FGVC-Aircraft")

# Launch the App
session = fo.launch_app(dataset)
```


## Dataset Details

### Dataset Description

Fine-Grained Visual Classification of Aircraft (FGVC-Aircraft) is a benchmark dataset for the fine grained visual categorization of aircraft.

**Note** This data has been used as part of the ImageNet FGVC challenge in conjuction with the International Conference on Computer Vision (ICCV) 2013. Test labels were not made available until the challenge due to the ImageNet challenge policy. They have now been released as part of the download above. If you arelady downloaded the iamge archive and want to have access to the test labels, simply download the annotations archive again.

**Note** Images in the benchmark are generously made available for non-commercial research purposes only by a number of airplane spotters. Please note that the original authors retain the copyright of the respective photographs and should be contacted for any other use. For further details see the copyright note below.


- **Language(s) (NLP):** en
- **License:** other

### Dataset Sources

<!-- Provide the basic links for the dataset. -->

- **Homepage:** https://www.robots.ox.ac.uk/~vgg/data/fgvc-aircraft/#format
- **Paper:** [Towards a Detailed Understanding of Objects and Scenes in Natural Images](http://www.clsp.jhu.edu/workshops/archive/ws-12/groups/tduosn/)


## Dataset Structure

The dataset contains 10,200 images of aircraft, with 100 images for each of 102 different aircraft model variants, most of which are airplanes. The (main) aircraft in each image is annotated with a tight bounding box and a hierarchical airplane model label.

Aircraft models are organized in a four-levels hierarchy. The four levels, from finer to coarser, are:

- **Model**, e.g. *Boeing 737-76J*. Since certain models are nearly visually indistinguishable, this level is not used in the evaluation.
- **Variant**, e.g. *Boeing 737-700*. A variant collapses all the models that are visually indistinguishable into one class. The dataset comprises 102 different variants.
- **Family**, e.g. *Boeing 737*. The dataset comprises 70 different families.
- **Manufacturer**, e.g. *Boeing*. The dataset comprises 41 different manufacturers.

The data is divided into three equally-sized training, validation and test subsets. The first two sets can be used for development, and the latter should be used for final evaluation only. The format of the data is described next.

## Dataset Creation

<!-- This section describes the people or systems who originally created the data. It should also include self-reported demographic or identity information for the source data creators if this information is available. -->

The creation of this dataset started during the Johns Hopkins CLSP Summer Workshop 2012 [Towards a Detailed Understanding of Objects and Scenes in Natural Images](http://www.clsp.jhu.edu/workshops/archive/ws-12/groups/tduosn/) with, in alphabetical order, Matthew B. Blaschko, Ross B. Girshick, Juho Kannala, Iasonas Kokkinos, Siddharth Mahendran, Subhransu Maji, Sammy Mohamed, Esa Rahtu, Naomi Saphra, Karen Simonyan, Ben Taskar, Andrea Vedaldi, and David Weiss.

The CLSP workshop was supported by the National Science Foundation via Grant No 1005411, the Office of the Director of National Intelligence via the JHU Human Language Technology Center of Excellence; and Google Inc.

A special thanks goes to Pekka Rantalankila for helping with the creation of the airplane hieararchy.

Many thanks to the photographers that kindly made available their images for research purposes. Each photographer is listed below, along with a link to his/her [airlners.net](http://airliners.net/) page:

- [Mick Bajcar](http://www.airliners.net/profile/dendrobatid)
- [Aldo Bidini](http://www.airliners.net/profile/aldobid)
- [Wim Callaert](http://www.airliners.net/profile/minoeke)
- [Tommy Desmet](http://www.airliners.net/profile/tommypilot)
- [Thomas Posch](http://www.airliners.net/profile/snorre)
- [James Richard Covington](http://www.airliners.net/profile/lemonkitty)
- [Gerry Stegmeier](http://www.airliners.net/profile/stegi)
- [Ben Wang](http://www.airliners.net/profile/aal151heavy)
- [Darren Wilson](http://www.airliners.net/profile/dazbo5)
- [Konstantin von Wedelstaedt](http://www.airliners.net/profile/fly-k)
- 
Please note that the images are made available **exclusively for non-commercial research purposes**. The original authors retain the copyright on the respective pictures and should be contacted for any other usage of them.

## Citation
<!-- If there is a paper or blog post introducing the dataset, the APA and Bibtex information for that should go in this section. -->

**BibTeX:**

```bibtex
@techreport{maji13fine-grained,
   title         = {Fine-Grained Visual Classification of Aircraft},
   author        = {S. Maji and J. Kannala and E. Rahtu
                    and M. Blaschko and A. Vedaldi},
   year          = {2013},
   archivePrefix = {arXiv},
   eprint        = {1306.5151},
   primaryClass  = "cs-cv",
}
```

## Dataset Card Author

[Jacob Marks](https://huggingface.co/jamarks)
Output:
{
    "extracted_code": "import fiftyone as fo\nimport fiftyone.utils.huggingface as fouh\n\n# Load the dataset\n# Note: other available arguments include 'max_samples', etc\ndataset = fouh.load_from_hub(\"Voxel51/FGVC-Aircraft\")\n\n# Launch the App\nsession = fo.launch_app(dataset)"
}
