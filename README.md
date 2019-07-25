# BIOMETRIC-RECOGNITION-USING-GAIT-ANALYSIS
This project ....

# Requirements
The code was written in Python 3.5, but it is probably also compatible with other versions.

# Python packages
1) TensorFlow 1.3 - how to install (however, some parts of code may be compatible with lower version, report an issue if you would have any problems.)
2) numpy, scipy, PIL

# Basic information about architecture
The network takes raw RGB video frames of a pedestrian as an input and produces one-dimensional vector - gait descriptor that exposes as an identification vector. The identification vectors from gaits of each two different people should be linearly separable. Whole network consists of two sub-networks connected in cascade - HumanPoseNN and GaitNN.

Spatial features from the video frames are extracted according to the descriptors that involve pose of the pedestrian. These descriptors are generated from the first sub-network - HumanPoseNN defined in human_pose_nn module. HumanPoseNN can be also used as a standalone network for regular 2D pose estimation problem from still images (for more info see this section).

Responsibility of the second sub-network - GaitNN defined in gait_nn module is the further processing of the generated spatial features into one-dimensional pose descriptors with the use of a residual convolutional network. Temporal features are then extracted across these pose descriptors with the use of the multilayer recurrent cells - LSTM or GRU. All temporal features are finally aggregated with Average temporal pooling into one-dimensional identification vector with good discriminatory properties. As already mentioned in the text above, the human identification vectors are linearly separable with each other and can therefore be classified with e.g. linear SVM.

# Pre-trained models
HumanPoseNN: MPII + LSP
Download: MPII+LSP.ckpt (https://drive.google.com/file/d/1bNoZkuI0TCqf_DV613SOAng3p6Y0Si6a/view)

The checkpoint MPII+LSP.ckpt was trained on images from MPII and LSP database. In the graph below you can see the average distance between predicted and desired joints on a validation set of about 6 000 images.

HumanPoseNN: Human 3.6m
Download: Human3.6m.ckpt (action walking)(https://drive.google.com/file/d/1lup13q5lTzsbrRZafpNbVF8uUyblMpZ3/view)

The checkpoint Human3.6m.ckpt was trained on the database Human 3.6m and only on the walking sequences of peoples S1, S6, S7, S8, S9 and S11 (48 sequences). 

