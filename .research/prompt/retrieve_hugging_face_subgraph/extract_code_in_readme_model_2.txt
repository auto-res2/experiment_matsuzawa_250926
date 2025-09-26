
Input:
From the Hugging Face README provided in “# README,” extract and output only the Python code required for execution. Do not output any other information. In particular, if no implementation method is described, output an empty string.

# README
---
tags:
- clip
- siglip
library_name: open_clip
pipeline_tag: zero-shot-image-classification
license: apache-2.0
datasets:
- webli
---
# Model card for ViT-B-16-SigLIP-i18n-256

A SigLIP (Sigmoid loss for Language-Image Pre-training) model trained on WebLI.

This model has been converted to PyTorch from the original JAX checkpoints in [Big Vision](https://github.com/google-research/big_vision). These weights are usable in both OpenCLIP (image + text) and timm (image only).

## Model Details
- **Model Type:** Contrastive Image-Text, Zero-Shot Image Classification.
- **Original:** https://github.com/google-research/big_vision
- **Dataset:** WebLI
- **Papers:**
  - Sigmoid loss for language image pre-training: https://arxiv.org/abs/2303.15343

## Model Usage
### With OpenCLIP
```
import torch
import torch.nn.functional as F
from urllib.request import urlopen
from PIL import Image
from open_clip import create_model_from_pretrained, get_tokenizer # works on open-clip-torch>=2.23.0, timm>=0.9.8

model, preprocess = create_model_from_pretrained('hf-hub:timm/ViT-B-16-SigLIP-i18n-256')
tokenizer = get_tokenizer('hf-hub:timm/ViT-B-16-SigLIP-i18n-256')

image = Image.open(urlopen(
    'https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/beignets-task-guide.png'
))
image = preprocess(image).unsqueeze(0)

labels_list = ["a dog", "a cat", "a donut", "a beignet"]
text = tokenizer(labels_list, context_length=model.context_length)

with torch.no_grad(), torch.cuda.amp.autocast():
    image_features = model.encode_image(image)
    text_features = model.encode_text(text)
    image_features = F.normalize(image_features, dim=-1)
    text_features = F.normalize(text_features, dim=-1)

    text_probs = torch.sigmoid(image_features @ text_features.T * model.logit_scale.exp() + model.logit_bias)

zipped_list = list(zip(labels_list, [round(p.item(), 3) for p in text_probs[0]]))
print("Label probabilities: ", zipped_list)
```

### With `timm` (for image embeddings)
```python
from urllib.request import urlopen
from PIL import Image
import timm

image = Image.open(urlopen(
    'https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/beignets-task-guide.png'
))

model = timm.create_model(
    'vit_base_patch16_siglip_256',
    pretrained=True,
    num_classes=0,
)
model = model.eval()

# get model specific transforms (normalization, resize)
data_config = timm.data.resolve_model_data_config(model)
transforms = timm.data.create_transform(**data_config, is_training=False)

output = model(transforms(image).unsqueeze(0))  # output is (batch_size, num_features) shaped tensor
```    

## Citation
```bibtex
@article{zhai2023sigmoid,
  title={Sigmoid loss for language image pre-training},
  author={Zhai, Xiaohua and Mustafa, Basil and Kolesnikov, Alexander and Beyer, Lucas},
  journal={arXiv preprint arXiv:2303.15343},
  year={2023}
}
```
```bibtex
@misc{big_vision,
  author = {Beyer, Lucas and Zhai, Xiaohua and Kolesnikov, Alexander},
  title = {Big Vision},
  year = {2022},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/google-research/big_vision}}
}
```

Output:
{
    "extracted_code": "import torch\nimport torch.nn.functional as F\nfrom urllib.request import urlopen\nfrom PIL import Image\nfrom open_clip import create_model_from_pretrained, get_tokenizer # works on open-clip-torch>=2.23.0, timm>=0.9.8\n\nmodel, preprocess = create_model_from_pretrained('hf-hub:timm/ViT-B-16-SigLIP-i18n-256')\ntokenizer = get_tokenizer('hf-hub:timm/ViT-B-16-SigLIP-i18n-256')\n\nimage = Image.open(urlopen(\n    'https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/beignets-task-guide.png'\n))\nimage = preprocess(image).unsqueeze(0)\n\nlabels_list = [\"a dog\", \"a cat\", \"a donut\", \"a beignet\"]\ntext = tokenizer(labels_list, context_length=model.context_length)\n\nwith torch.no_grad(), torch.cuda.amp.autocast():\n    image_features = model.encode_image(image)\n    text_features = model.encode_text(text)\n    image_features = F.normalize(image_features, dim=-1)\n    text_features = F.normalize(text_features, dim=-1)\n\n    text_probs = torch.sigmoid(image_features @ text_features.T * model.logit_scale.exp() + model.logit_bias)\n\nzipped_list = list(zip(labels_list, [round(p.item(), 3) for p in text_probs[0]]))\nprint(\"Label probabilities: \", zipped_list)\n\nfrom urllib.request import urlopen\nfrom PIL import Image\nimport timm\n\nimage = Image.open(urlopen(\n    'https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/beignets-task-guide.png'\n))\n\nmodel = timm.create_model(\n    'vit_base_patch16_siglip_256',\n    pretrained=True,\n    num_classes=0,\n)\nmodel = model.eval()\n\n# get model specific transforms (normalization, resize)\ndata_config = timm.data.resolve_model_data_config(model)\ntransforms = timm.data.create_transform(**data_config, is_training=False)\n\noutput = model(transforms(image).unsqueeze(0))  # output is (batch_size, num_features) shaped tensor"
}
