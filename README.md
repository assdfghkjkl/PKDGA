# Introduction

This repository contains the implementations of PDKGA and its competitors. PKDGA is an adversarial domain generation algorithm that uses partial knowledge of the target detector for reinforcement learning training. Its overall achitecture is depected as follows. 

<p align="center">
 <img src="https://github.com/abcdefdf/PKDGA/assets/98793069/b6c50a2a-488d-4901-a42e-98896384d29e" width="600px" />
<p>


# Installation and Usage Hints
PKDGA is created, trained and evaluated on Ubuntu 16.04 or Win10 using Python.

# DGA Reproducibility
## PKDGA
### Create a anaconda environment:

*conda create -n <environment_name> pytohn==3.7*  //**environment_name** is the name of the created environment 

### Install the required packages:

*pip -r install requirement.txt*

### Pre-train the target domain detector
 Select a target detector and train it to detect malicious domains. The detailed command for training each detector will be shown in the **Detector Reproducibilition** part.

The screenshots during pretraining target detector：
<p align="center">
 <img src="https://github.com/abcdefdf/PKDGA/assets/98793069/6c389df8-cc9c-4b81-b755-4f007cd2863b" />
<p>
  
### Training PKDGA to compromise the target detector

*python pkdga/gen_model.py*

The screenshots during training PKDGA is

<p align="center">
 <img src="https://github.com/abcdefdf/PKDGA/assets/98793069/f00f3f3f-f3ed-4314-a7bd-72969678a1ba" />
<p> 

### Generate domains using PKDGA

*python gen_sample.py*

Some samples(2rd-level domains only) are shown as follows:
  
<streflix\>
<notgichtirnax\>
<ecawerdaille\>
<porete\>
<cridmi\>
<ifireda\>
<xlazairan\>
<youregan\>
<pathrovegalima\>
<porcedch\>
<omehmswime\>
<pardesleatress\>
<migoo\>
<fintstalnotic\>
<zpus-animesops\>
<hatporhsaviaker\>
<yudija\>
<dinyrimesbot\>
<elinkbilyimen1\>
<latorb\>
<jahas\>
<sbagebissear\>
<bashiammy\>
<loguo\>
<notebonlop\>
<intarasbing\>
<otoulaa\>
<byirbaotive\>
<tvhjemborodop\>
<tenihahang\>\>
<nrfwedreeke\>
<mnex\>
<mreelcagazun\>
<pred\>
<latana\>
<clive-tipanews\>
<lowpek\>
<voithh\>
<petcolf\>
<svvertenexvedes\>
<gastrafro\>

## The usages of the rest files in *PKDGA/* are introduced as follows. 

### rollout.py: 
  
The fuction of computing policy-based gradient, which makes the token sequence Y resist against target detector D. It is called by the *gen_model.py* when training PKDGA.

### exp1.py:
 The experimental code of measuring DGAs' evasoin ability, the results are shows as follows:
 
 
 <p align="center">
 <img src="https://github.com/abcdefdf/PKDGA/assets/98793069/4f0729ea-6580-4e0d-ad28-f423a7ec7339"  width="500px"/>
<p> 

 
 

### exp2.py: 
 
The experimental code of measuring training sets' impacts on PKDGA, the results are shown as follows: 
 
  <p align="center">
 <img src="https://github.com/abcdefdf/PKDGA/assets/98793069/8d622f7a-6644-4b65-9738-2c4adf6e4478" width="800px"/>
<p> 



## khaos khaos[1]

### Introduction: 

DGA, builds a dictionary containing n-grams of legitimate domain names and trains a wasserstein generative adversarial network (WGAN) to synthesize domain names by merging the sampled n-grams. In our implementation, we set the embedding size of n-grams to 5,000. The domain synthesizer and the discriminator are implemented using the residual convolutional network.

### Usage: 
 
 *python khaos/gan_language.py*

# Detector Reproducibility
## FANCI[2]
 
### Introduction: 

 DGA detector, it extracts 21 lightweight DGA features, including structural, linguistic and statistical features, and employs a supervised model (Random Forest) for classification.
###Usage: 

 *python RF/RF_classifier.py*

## bilstm,lstm,textcnn [3]
### Introduction: 
 DGA detector, directly leverage neural networks to distinguish AGDs from benign ones without extracting features manually.

### Usage:
 
*python lstm/lstm_class.py -layer -emb -hid -device* // **layer** is the layer number of the network, **emb** is the embedding size, **hid** is the size of hidden layer.
 
*python textcnn/cnn.py*  -device
 
*python bilstm/bilstm.py -max_features - maxlen -device*  // **maxlen** is the maximal length of domain names.
 
## graph [4]
### Introduction: 
 
Graph is able to detect dictionary-based AGDs that are generated by concatenating words from a predefined dictionary. It constructs a graph describing the relationships between the largest common substrings in a domain and the graph with average degrees larger than a threshold is considered as malicious. In our implementation, the substrings that repeat more than three times are considered as basic words, and the degree threshold is set to 3.

### Usage:
 
 *python graph/WordGraph.py*
 
## Statics [5]
### Introduction:  
DGA detector, argues that AGDs follow different distributions from the legitimate domain names. A domain is identified as benign if it has a negligible distance from the legitimate domains. In particular, it measures the distance using Kullback-Leibler divergence, Jaccard index and Edit distance.

### Usage:
 *python statics/statics.py*
 
# Disclaimer
This project is still under development and may be missing at the moment. In addition, some paths may require you to modify.
 
# Reference
[1] X. Yun, J. Huang, Y. Wang, T. Zang, Y. Zhou, and Y. Zhang, “Khaos: An adversarial neural network dga with high anti-detection ability,” IEEE
Trans. Inf. Forensics Secur., vol. 15, no. 1, pp. 2225–2240, 2020.
 
[2] S. Schuppen, D. Teubert, P. Herrmann, and U. Meyer, “FANCI : Feature-based automated nxdomain classification and intelligence,” in Proc. USENIX Secur. Symp., 2018, pp. 1165–1181.
 
[3] J. Woodbridge, H. S. Anderson, A. Ahuja, and D. Grant, “Predicting domain generation algorithms with long short-term memory networks,” arXiv, 2016.
 
[4] M. Pereira, S. Coleman, B. Yu, M. DeCock, and A. Nascimento, “Dictionary extraction and detection of algorithmically generated domain names in passive dns traffic,” in Proc. Int. Symp. Res. in Attacks, Intrusions, and Defenses, 2018, pp. 295–314.
 
[5] S. Yadav, A. K. K. Reddy, A. L. N. Reddy, and S. Ranjan, “Detecting algorithmically generated domain-flux attacks with dns traffic analysis,” IEEE/ACM Trans. Netw., vol. 20, no. 5, pp. 1663–1677, 2012.
