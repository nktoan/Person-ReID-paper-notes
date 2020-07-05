# OS-Net
## Introduction
Since person re-identification is regarded as an instance-level recognition problem, it faces with two primary challenges: the **intra-class (instance/identity) variations** due to the changes of camera viewing conditions, and the **small inter-class variations** such as people in public space often wear similar clothes. To combat against these challenge, the model have to learn **discriminative features**. The authors argued such features need to be of *omni-scales*, defined as the combination of variable homogeneous scales and heterogeneous scales, each of which is composed of a mixture of multiple scales.

The authors propose **OS-Net**, a novel CNN architecture designed for learning omni-scale feature representations. In their method, they construct building block consists of multiple convolutional streams with different receptive field sizes. The feature scale that each stream extracts determined by *exponent* (a dimension factor that is linearly increased across streams to ensure that various scales are captured in each block). In addition, the authors use a unified aggregation gate (**AG**) to dynamically combine the resulting multi-scale feature maps. It is a mini-network sharing parameters across all streams, by training AG, the generated channel-wise weights become input-dependent, hence the dynamic scale fusion. 

Besides, the authors aim to construct a *lightweight* network. Instead of sending the raw videos to
a central server, only the extracted features need to be sent. Therefore, small re-ID networks are preferred. In order to do this, in their building block, they factorize convolutions with pointwise and depthwise convolutions.
## Related Work

## Omni-Scale Feature Learning
### Depthwise Separable Convolutions
- Aim to focus on person-related features and eliminating irrelevant backgrounds.
- **Channel Attention Module (CAM)**: The main purpose of designing CAM is to group and to aggregate semantically similar channels that are obtained from a trained **CNN** classifier. 

<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/cam_image.png" />
</p>
<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/cam_detail.png" />
</p>

- **Position Attention Module (PAM)**: The main purpose of designing PAM to capture and aggregate semantically related pixels in the spatial domain. 

<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/pam_image.png" />
</p>
<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/pam_detail.png" />
</p>

### Diversity through Orthogonality Regularization
- The authors carry out the diversity via orthogonality, then obtain a novel orthogonality regularizer term. It is applied to both hidden features and weights, of both convolutional and fully connected layers. Orthogonality regularizer on feature space (**O.F**) is to reduce feature correlations. Orthogonality regularizer on weight (**O.W**) encourages filter diversity, thereby enhances the learning capacity.

<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/reshape.png" />
</p>

- The problem with many orthogonality methods is the **SVD** computing costs are expensive, urging for soft orthogonality regularizers. Many existing regularizers restrict the **Gram matrix** of **F** to be close to an identity matrix under Frobenius norm that can avoid the **SVD** step while being differentiable, but this method cause regularizers biased due to rank deficiency.

<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/orthogonality_regularization.png" />
</p>

### Network Architecture
- **ABD-Net** is compatible with most common feature extraction backbones, such as **ResNet, InceptionNet, and DenseNet**. Here, the authors use the **ResNet** network since it is the most common one used in the problem Person-Reid.

<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/network_architecture.png" />
</p>

- **Loss function**: comprises of a cross-entropy loss, a hard mining triplet loss, and orthogonal constraints on feature (**O.F**) and on weights (**O.W**) penalty: 

<p align="center">
  <img src="https://github.com/soloSquad1999/Person-ReID-paper-notes/blob/master/Network%20Approach/ABD-Net/loss_center.png" />
</p>

## Experiment Results
- On **DukeMTMC-Reid**, **ABD-Net** obtains *78.59% mAP*, whereas it achieves *88.28% mAP* on **Market-1501**. Especially, on **MSMT17**, it obtains *60.8% mAP*, which is currently the top-1 accuracy. 
