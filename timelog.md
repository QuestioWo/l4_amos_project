# Timelog

* Abdominal multi-organ segmentation using deep neural networks (CT)
* Jim Carty
* 2462934C
* Dr. Ali Gooya

## Guidance

* This file contains the time log for your project. It will be submitted along with your final dissertation.
* **YOU MUST KEEP THIS UP TO DATE AND UNDER VERSION CONTROL.**
* This timelog should be filled out honestly, regularly (daily) and accurately. It is for *your* benefit.
* Follow the structure provided, grouping time by weeks.  Quantise time to the half hour.

## Week 1

### 28th Sept 2022

* *0.5 hours* meeting with supervisor
* *1 hour* downloading data and data visualisation tools

## 30th Sept 2022 

* *2 hour* setting up project template, watching introduction session and continuing with data investigation

## 3rd Oct 2022

* *1 hour* experimenting with prebuilt tensorflow segmentation CNNs. discovered I will likely have to make/confgure my own since majority take 3-channel matrices aka RGB images, not arbitrary 3D matrices

## 4th Oct 2022

* *2.5 hours* researching segmentation deep NNs, tensorflow used UNet so I mainly investigated that. found [a UNet implementation that works for 3D single-channel medical images](https://github.com/davidiommi/Pytorch--3D-Medical-Images-Segmentation--SALMON), i.e what my project is meant to be. worked on trying to get it working/training to see its results to evaluate its efficacy

## 5th Oct 2022

* *0.75 hours* weekly meeting and discussion/clarification of goals. identified spatially-aware/4D CNNs as a possible avenue for research this week, along with training and viewing the results of the current CNN approaches to see their shortcomings

## 8th Oct 2022

* *1 hour* formatting data for use with exisiting models and setting up system for training as collab does not have storage capacity. took a while due to data capacity requirements

## 11th Oct 2022

* *2 hours* researching 4D CNNs, medical imaging literature and attempting to train model.

## 12th Oct 2022

* *0.5 hours* researching edge-based segmentation

## 19th Oct 2022

* *2 hours* general research trying to find interesting/relevant papers on vision transformers, attention maps, and spatially-aware cnns

## 20th Oct 2022

* *2 hours* fully reading papers found yesterday and writing up notes and descriptions of them
* *0.5 hours* meeting with Dr. Gooya

## 26th Oct 2022

* *2 hours* researching transformers, how they work and the current research in the field

## 27th Oct 2022

* *3 hours* further research on machine learning techniques, found out about Perciever IO from deepmind and about swin tranformers and how 3d swin networks have already been done. also looked into similarity scores for imagenette for comparisons

* *0.25 hours* advisor meeting

## 2nd November 2022

* *2 hours* research into Perciever code and for BTSwin-UNet code.

## 3rd November 2022

* *0.5 hours* advisor meeting

## 8th November 2022

* *4 hours* getting to grips with pytorch perceiver IO code and beginning extending it to add a new segmentation image model

## 15th Novemeber 2022

* *8 hours* added ability for existing perceiver-io code to load miccai dataset and added basic framework for basic preprocessing

## 23rd November 2022

* *5 hours* working on automatically coregistering all images as a preprocessing step to help the network better form self attentions. tried multiple solutions using itk and selected one as acceptable. having scaling issues as currently only interpolating width and height, not depth

## 5th December 2022

* *4 hours* working on coregistration, fixed scaling issues and results seem good. now have to integrate experimentation with current micca loader and preprocess the entire dataset as is costly each time it is done

## 7th December 2022

* *3 hours* integrating and verifying coregistration preprocessing in data loader
* *2 hours* preparing and beginning work on making new model for inferencing

## 12th December 2022

* *5 hours* model now working for 2d scan. appears that validation set is not splitting from training properly - will have to fix. and will have to evaluate results.

## 15th December 2022

* *6 hours* revisiting preprocessing to correctly register images with scaling in mind to make sure inferences, trainign and evaluations are sound

## 16th December 2022

* *6 hours* finalising preprocessing to verify that rescalings are correct and that scans/segmentations are interpolated correctly using nearest neighbour (to avoid incorrect partial labels at boundaries). looking into removing the backgorund label from consideration in the loss functions so that the model actually trains to segment organs

## 18th December 2022

* *4 hours* made new loss function that can take the backgrounds affect/incorrectness into account better. got inference script displaying images correctly plus the differences between the GT labels and the predictions. currently explanding everything to be able to handle multiple slices images - starting with a viewer for the inference script

## 19th December 2022

* *4 hours* re-preprocessed data to be better coregistered. got model working, training and inferencing for 3d images - had to half image resolution from 256->128. setting up for large training run. also got working on google colab as larger network required more vram

## 20th December 2022

* *2 hours* changing how outputs are perceived as classifications. verifying and updating new loss function and starting large run locally to hopefully actually see segmentations soon

## 31st December 2022

* *2 hours* preprocessed dataset with smaller size and configured for a larger model in an attempt to see new/novel/correct outputs. training started and may take a long time