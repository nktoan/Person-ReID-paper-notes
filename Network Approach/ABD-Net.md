ABD-Net: 
This is the state-of-the-art method training on the MSMT17 dataset. One of the most imperative things about this method is that they incorporate both “attentive” and “diverse” mechanisms on the feature embedding for the problem person Re-ID. Particularly, while the “attentive” mechanism aims to correct misalignment, eliminate background perturbance, and focus on discriminative local parts of body appearances, the “diverse” one aims to encourage lower correlation between features which be claimed to boost the matching performance, thereby potentially make feature space more comprehensive. The authors propose Attention but Diverse Network (ABD-Net), the main contributions of ABD-Net are listed below:
Attention mechanisms: comprises of Channel Attention Module (CAM) and Position Attention Module (PAM). CAM supports channel-wise, feature-level information aggregation, whereas PAM captures the spatial awareness of body and part positions by mainly capture the discriminative appearances of certain body parts.
Spectral value difference orthogonality (SVDO): manipulate the condition number of the weight Gram matrix as applied to both activations and weights, which leads to reduce learned feature correlations.
Attention though Channel-Wise and Position-Wise: aim to focus on person-related features and eliminating irrelevant backgrounds.
Channel Attention Module (CAM): The main purpose of designing GAM is to group and to aggregate semantically similar channels that are obtained from a trained CNN classifier. 


	

Position Attention Module (PAM): The main purpose of designing GAM to capture and aggregate semantically related pixels in the spatial domain. 


Diversity through Orthogonality Regularization: The authors carry out the diversity via orthogonality, then obtain a novel orthogonality regularizer term. It is applied to both hidden features and weights, of both convolutional and fully connected layers. Orthogonality regularizer on feature space (O.F) is to reduce feature correlations. Orthogonality regularizer on weight (O.W) encourages filter diversity, thereby enhances the learning capacity.
For features maps … 

Network Architecture: ABD-Net is compatible with most common feature extraction backbones, such as ResNet, InceptionNet, and DenseNet. Here, the authors use the ResNet network since it is the most common one in the problem Person-Reid.


Loss function L: comprises of a cross-entropy loss, a hard mining triplet loss, and orthogonal constraints on feature (O.F.) and on weights (O.W.) penalty: ….(LATEX).
Experiments Results: On DukeMTMC-Reid, ABD-Net obtains 78.59% mAP, whereas it achieves 88.28% mAP on Market-1501. Especially, on MSMT17, it obtains 60.8% mAP, which is currently the top-1 accuracy. 

