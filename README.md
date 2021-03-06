# Multi-Task Deep Neural Networks for Natural Language Understanding

This PyTorch package implements the Multi-Task Deep Neural Networks (MT-DNN) for Natural Language Understanding, as described in:

Xiaodong Liu\*, Pengcheng He\*, Weizhu Chen and Jianfeng Gao<br/>
Multi-Task Deep Neural Networks for Natural Language Understanding<br/>
[arXiv version](https://arxiv.org/abs/1901.11504) <br/>
\*: Equal contribution


## Quickstart 

### Setup Environment
#### Install via pip:
1. python3.6

2. install requirements </br>
   ```> pip install -r requirements.txt```

#### Use  docker:
1. pull docker </br>
   ```> docker pull allenlao/pytorch-mt-dnn:v0.1```

2. run docker </br>
   ```> docker run -it --rm --runtime nvidia  allenlao/pytorch-mt-dnn:v0.1 bash``` </br>
    Please refere the following link if you first use docker: https://docs.docker.com/

### Train a toy MT-DNN model
1. download data </br>
   ```> sh download.sh``` </br>
   Please refer to download GLUE dataset: https://gluebenchmark.com/

2. preprocess data </br>
   ```> python prepro.py```

3. training </br>
   ```> python train.py```

**Note that we ran experiments on 4 V100 GPUs for base mt-dnn models. You may need to reduce batch size for other GPUs.** <br/>

### GLUE Result reproduce
1. MTL refinement: refine MT-DNN (shared layers), initialized with the pre-trained BERT model, via MTL using all GLUE tasks excluding WNLI to learn a new shared representation. </br>
**Note that we ran this experiment on 8 V100 GPUs (32G) with a batch size of 32.**
   + Preprocess GLUE data via the aforementioned script
   + Training: </br>
   ```>scripts\run_mt_dnn.sh```

2. Finetuning: finetune MT-DNN to each of the GLUE tasks to get task-specific models. </br>
Here, we preovide two examples, STS-B and RTE. You can use similar scripts to finetune all the GLUE tasks. </br>
   + Finetune on the STS-B task </br>
   ```> scripts\run_stsb.sh``` </br>
   You should get about 90.5/90.4 on STS-B dev in terms of Pearson/Spearman correlation. </br>
   + Finetune on the RTE task  </br>
   ```> scripts\run_rte.sh``` </br>
   You should get about 83.8 on RTE dev in terms of accuracy. </br>  

### SciTail & SNIL Result reproduce (Domain Adaptation)
1. Domain Adaptation on SciTail  </br>
   ```>scripts\scitail_domain_adaptation_bash.sh```

2. Domain Adaptation on SNLI </br>
  ```>scripts\snli_domain_adaptation_bash.sh```

## Notes and Acknowledgments
BERT pytorch is from: https://github.com/huggingface/pytorch-pretrained-BERT <br/>
BERT : https://github.com/google-research/bert <br/>
We also used some code from: https://github.com/kevinduh/san_mrc <br/>

### How do I cite MT-DNN?

For now, please cite [arXiv version](https://arxiv.org/abs/1901.11504):

```
@article{liu2019mt-dnn,
  title={Multi-Task Deep Neural Networks for Natural Language Understanding},
  author={Liu, Xiaodong and He, Pengcheng and Chen, Weizhu and Gao, Jianfeng},
  journal={arXiv preprint arXiv:1901.11504},
  year={2019}
}

and a new version of the paper will be shared later. 
```
***Typo:*** there is no activation fuction in Equation 2. 
### Contact Information

For help or issues using MT-DNN, please submit a GitHub issue.

For personal communication related to MT-DNN, please contact Xiaodong Liu (`xiaodl@microsoft.com`), Pengcheng He (`penhe@microsoft.com`), Weizhu Chen (`wzchen@microsoft.com`) or Jianfeng Gao (`jfgao@microsoft.com`).
