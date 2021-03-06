# ContinualLocalReplacement
Continual local replacement is a simple yet effective method for few-shot image recognition.
This method is able to introduce more semantic information and significantly enlarge the supervised signals in embedded space for decision boundary learning. See T-SNE visualization and saliency maps below.
In T-SNE visualization, the labeled images (i.e. support set) and synthesized images are marked by stars and triangles, respectively.
During fine tuning, the embedded features change and can cover a larger area within each embedded cluster for learning.


This algorithm is based on standard transfer learning and thus it has a good scalability.
For example, it can be easily combined with the weight imprinting technique.

This repository includes the source codes of ContinualLocalReplacement and its weight imprinting variant.
Please check our original paper for more algorithm details.

<div align="center">
<img src="https://raw.githubusercontent.com/PaperID-4824/ContinualLocalReplacement/master/images/tsne_visualization2.gif" height="300px" alt="demo2" >
<img src="https://raw.githubusercontent.com/PaperID-4824/ContinualLocalReplacement/master/images/tsne_visualization1.gif" height="300px" alt="demo1" >
</div>

![demo3](https://raw.githubusercontent.com/PaperID-4824/ContinualLocalReplacement/master/images/saliency_map.png)


# 1. Prerequisites
This code is implemented on Pytorch. 
So you may need to install
* Python 3.x
* Pytorch 1.0.0 or above

We have tested this code on Ubuntu and Windows10 x64 operation system.


# 2. Run 
Run codes using below commands. 
We conduct all experiments on default hyper-parameters. But you may try other hyper-parameters.
For example, you can actually achieve better performance than the reported results when you test imprint_jigsaw method with jig_replace_max_num=9 on CUB dataset.

We also provide the driver scripts. Please check the run_scripts folder.

Organize Dataset
------------
Before runing, please check the code to make sure all pathes set correctly.
```
python ./filelists/miniImagenet/write_data_json.py
python ./filelists/tieredImagenet/write_data_json.py
python ./filelists/CUB/write_data_json.py
python ./filelists/caltech256/write_data_json.py
```


Training
------------
```
python ./train.py --dataset miniImagenet/tieredImagenet/CUB/caltech256 --method jigsaw --test_n_way 5 --n_shot 5 --gpu 0
python ./train.py --dataset miniImagenet/tieredImagenet/CUB/caltech256 --method imprint_jigsaw --test_n_way 5 --n_shot 5 --gpu 0
```

Testing
------------
```
python ./test.py --dataset miniImagenet/tieredImagenet/CUB/caltech256 --method jigsaw --test_n_way 5 --n_shot 1 --gpu 1
python ./test.py --dataset miniImagenet/tieredImagenet/CUB/caltech256 --method jigsaw --test_n_way 5 --n_shot 5 --gpu 1
python ./test.py --dataset miniImagenet/tieredImagenet/CUB/caltech256 --method imprint_jigsaw --test_n_way 5 --n_shot 1 --gpu 1
python ./test.py --dataset miniImagenet/tieredImagenet/CUB/caltech256 --method imprint_jigsaw --test_n_way 5 --n_shot 5 --gpu 1
```

# 3. Datasets and Pre-trained Parameters
We provide our pre-trained parameters for reproducing the results in the paper.
You can download them from [HERE](https://drive.google.com/open?id=1Jpm5EVYAssa-NapMrkEgk5gM5p6o-tkD).

Since the datasets are large, we don't provide them here. 
But they are publicly accessiable from the Internet.


