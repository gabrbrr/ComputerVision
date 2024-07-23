# ComputerVision
Computer vision's project repository
# Introduction
Pedestrian crossing intention estimation is an essential task for improving road safety in autonomous driving and smart transportation systems. This task focuses on predicting whether a pedestrian plans to cross the street, allowing vehicles to react appropriately. By using data from visual signals, movement patterns, and surrounding context, the system can better understand pedestrian behavior. This project aims at understanding how different types of input might prove beneficial.
# Dataset 
Here i use the PIE Dataset, 6 hours of continuous 1080p footage recorded in Toronto, Canada in clear weather with annotations of, for what we’re concerned, pedestrian bounding boxes and vehicle speed.
In particular we adopt the benchmark introduced by Kotseruba et al. where the observation sequences are 16 frames (0.5 seconds) taken in the range [76,46] before the TTE (pedestrian starts crossing) with an overlap of 0.6 in training to increase number of samples.
After these steps, we’re left with the following dataset:\n
Train: 		2315 No Crossing	           765 Crossing
Validation: 	252 No Crossing		52 Crossing\n
Test: 		690 No Crossing                   252 Crossing.\n
It can be seen that the data  is quite imbalanced.
# Models
To study the effect of different types of input i did the following:
Finetuned a Resnet101 (pretrained on ImageNet) on the last frame of each sequence by using the cropped 2x 224x224 image around the pedestrian.
Finetuned a C3D network (pretrained on Sports) 1Mwith the whole 16 frames by using the cropped 1.5x with 112x112
Trained the same C3D network in combination with an LSTM passing speed as input to it. Specific details are in the code.
The results are visible at the following link: https://wandb.ai/pamfil-1938844/CV?nw=nwuserpamfil1938844

N.B.To preprocess the dataset which can be handled through the PIE data interface (https://github.com/aras62/PIE) i used some functions from the benchmark (https://github.com/ykotseruba/PedestrianActionBenchmark) , in particular for resizing and cropping and for computing overlapping frames.




