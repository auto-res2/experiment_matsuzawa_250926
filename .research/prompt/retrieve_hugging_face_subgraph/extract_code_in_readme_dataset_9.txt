
Input:
From the Hugging Face README provided in “# README,” extract and output only the Python code required for execution. Do not output any other information. In particular, if no implementation method is described, output an empty string.

# README
---
license: mit
task_categories:
- image-classification
language:
- en
tags:
- legal
pretty_name: The Street View House Numbers (SVHN) Dataset
size_categories:
- 10K<n<100K
dataset_info:
  - config_name: default
    features:
      - name: image
        dtype: image
      - name: label
        sequence:
          - name: digit
            dtype: uint8
          - name: left
            dtype: float32
          - name: top
            dtype: float32
          - name: width
            dtype: float32
          - name: height
            dtype: float32
    splits:
      - name: train
        num_bytes: 7718427
        num_examples: 33402
      - name: test
        num_bytes: 2955196
        num_examples: 13068
    download_size: 685311858
    dataset_size: 10673623
configs:
  - config_name: default
    data_files:
      - split: train
        path: default/train/data-*.arrow
      - split: test
        path: default/test/data-*.arrow
---

# Dataset card for SVHN
The Street View House Numbers (SVHN) dataset is a real-world image dataset developed and designed for machine learning and object recognition algorithms, and is characterized by low data preprocessing and formatting requirements. Similar to MNIST, SVHN contains images of small cropped numbers, but in terms of labeled data, SVHN is an order of magnitude larger than MNIST, comprising over 600,000 digital images. Unlike MNIST, SVHN deals with a much more challenging and unsolved real-world problem - recognizing numbers and strings of numbers in natural scene images. The dataset is derived from house numbers captured in Google Street View images.

## Usage
### By API
```python
from datasets import load_dataset

ds = load_dataset("Genius-Society/svhn")
for item in ds["train"]:
    print(item)

for item in ds["test"]:
    print(item)
```

### Not By API
```python
import os
import zipfile
import requests

def download_file(url, save_path):
    response = requests.get(url, stream=True)
    with open(save_path, 'wb') as file:
        for chunk in response.iter_content(chunk_size=1024):
            if chunk:
                file.write(chunk)

def unzip(zip_file_path, extract_to):
    with zipfile.ZipFile(zip_file_path, 'r') as zip_ref:
        for member in zip_ref.infolist():
            zip_ref.extract(member, extract_to)

if not os.path.exists('./data.zip'):
    download_file(
        'https://www.modelscope.cn/datasets/Genius-Society/svhn/resolve/master/data/svhn.zip',
        'data.zip'
    )

if not os.path.exists('./data'):
    unzip('data.zip', './')
```

## Maintenance
```bash
GIT_LFS_SKIP_SMUDGE=1 git clone git@hf.co:datasets/Genius-Society/svhn
cd svhn
```

## Mirror
<https://www.modelscope.cn/datasets/Genius-Society/svhn>

## References
[1] <a href="http://ufldl.stanford.edu/housenumbers">The Street View House Numbers (SVHN) Dataset</a><br>
[2] <https://github.com/Genius-Society/svhn_recognition>
Output:
{
    "extracted_code": "from datasets import load_dataset\n\nds = load_dataset(\"Genius-Society/svhn\")\nfor item in ds[\"train\"]:\n    print(item)\n\nfor item in ds[\"test\"]:\n    print(item)\n\nimport os\nimport zipfile\nimport requests\n\ndef download_file(url, save_path):\n    response = requests.get(url, stream=True)\n    with open(save_path, 'wb') as file:\n        for chunk in response.iter_content(chunk_size=1024):\n            if chunk:\n                file.write(chunk)\n\ndef unzip(zip_file_path, extract_to):\n    with zipfile.ZipFile(zip_file_path, 'r') as zip_ref:\n        for member in zip_ref.infolist():\n            zip_ref.extract(member, extract_to)\n\nif not os.path.exists('./data.zip'):\n    download_file(\n        'https://www.modelscope.cn/datasets/Genius-Society/svhn/resolve/master/data/svhn.zip',\n        'data.zip'\n    )\n\nif not os.path.exists('./data'):\n    unzip('data.zip', './')"
}
