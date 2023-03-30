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
 
### 30th Sept 2022 

* *2 hour* setting up project template, watching introduction session and continuing with data investigation
 
## Week 2
 
### 3rd Oct 2022

* *1 hour* experimenting with prebuilt tensorflow segmentation CNNs. discovered I will likely have to make/confgure my own since majority take 3-channel matrices aka RGB images, not arbitrary 3D matrices
 
### 4th Oct 2022

* *2.5 hours* researching segmentation deep NNs, tensorflow used UNet so I mainly investigated that. found [a UNet implementation that works for 3D single-channel medical images](https://github.com/davidiommi/Pytorch--3D-Medical-Images-Segmentation--SALMON), i.e what my project is meant to be. worked on trying to get it working/training to see its results to evaluate its efficacy

### 5th Oct 2022

* *0.75 hours* weekly meeting and discussion/clarification of goals. identified spatially-aware/4D CNNs as a possible avenue for research this week, along with training and viewing the results of the current CNN approaches to see their shortcomings
 
### 8th Oct 2022

* *1 hour* formatting data for use with exisiting models and setting up system for training as collab does not have storage capacity. took a while due to data capacity requirements
 
## Week 3
 
### 11th Oct 2022

* *2 hours* researching 4D CNNs, medical imaging literature and attempting to train model.

## Week 3

### 12th Oct 2022

* *0.5 hours* researching edge-based segmentation

## Week 4

### 19th Oct 2022

* *2 hours* general research trying to find interesting/relevant papers on vision transformers, attention maps, and spatially-aware cnns
 
### 20th Oct 2022

* *2 hours* fully reading papers found yesterday and writing up notes and descriptions of them
* *0.5 hours* meeting with Dr. Gooya

## Week 4

### 26th Oct 2022

* *2 hours* researching transformers, how they work and the current research in the field
 
### 27th Oct 2022

* *3 hours* further research on machine learning techniques, found out about Perciever IO from deepmind and about swin tranformers and how 3d swin networks have already been done. also looked into similarity scores for imagenette for comparisons

* *0.25 hours* advisor meeting

## Week 5

### 2nd November 2022

* *2 hours* research into Perciever code and for BTSwin-UNet code.
 
### 3rd November 2022

* *0.5 hours* advisor meeting

## Week 6

### 8th November 2022

* *4 hours* getting to grips with pytorch perceiver IO code and beginning extending it to add a new segmentation image model

## Week 7

### 15th Novemeber 2022

* *8 hours* added ability for existing perceiver-io code to load miccai dataset and added basic framework for basic preprocessing

## Week 8

### 23rd November 2022

* *5 hours* working on automatically coregistering all images as a preprocessing step to help the network better form self attentions. tried multiple solutions using itk and selected one as acceptable. having scaling issues as currently only interpolating width and height, not depth

## Week 9

## Week 10

### 5th December 2022

* *4 hours* working on coregistration, fixed scaling issues and results seem good. now have to integrate experimentation with current micca loader and preprocess the entire dataset as is costly each time it is done
 
### 7th December 2022

* *3 hours* integrating and verifying coregistration preprocessing in data loader
* *2 hours* preparing and beginning work on making new model for inferencing

## Week 11

### 12th December 2022

* *5 hours* model now working for 2d scan. appears that validation set is not splitting from training properly - will have to fix. and will have to evaluate results.
 
### 15th December 2022

* *6 hours* revisiting preprocessing to correctly register images with scaling in mind to make sure inferences, trainign and evaluations are sound
 
### 16th December 2022

* *6 hours* finalising preprocessing to verify that rescalings are correct and that scans/segmentations are interpolated correctly using nearest neighbour (to avoid incorrect partial labels at boundaries). looking into removing the backgorund label from consideration in the loss functions so that the model actually trains to segment organs
 
### 18th December 2022

* *4 hours* made new loss function that can take the backgrounds affect/incorrectness into account better. got inference script displaying images correctly plus the differences between the GT labels and the predictions. currently explanding everything to be able to handle multiple slices images - starting with a viewer for the inference script

## Week 12

### 19th December 2022

* *4 hours* re-preprocessed data to be better coregistered. got model working, training and inferencing for 3d images - had to half image resolution from 256->128. setting up for large training run. also got working on google colab as larger network required more vram
 
### 20th December 2022

* *2 hours* changing how outputs are perceived as classifications. verifying and updating new loss function and starting large run locally to hopefully actually see segmentations soon

## Week 13

### 31st December 2022

* *2 hours* preprocessed dataset with smaller size and configured for a larger model in an attempt to see new/novel/correct outputs. training started and may take a long time

## Semester 2: Week 1

### 3rd January 2023

* *1 hour* Changing network to operate on a 2d slice for now. changed network parameters a bit to make it easier to train. changed loss function using after further research. started new training run and results are actually producing reasonable-ish segmentations

### 4th January 2023

* *1 hour* refining model to decrease size and begining retraining. analysed scans from previous and current run

### 5th January 2023

* *1 hour* advisor meeting and halted network traing. re-preprocessing dataset to 128x128 and restarting training

### 8th January 2023

* *10 minutes* created new model configs and starting training on them

## Semester 2: Week 2

### 15th January 2023

* *1 hour* fixing inference script and standardising preprocessing interpolations and restarting preprocessing

## Semester 2: Week 3

### 17th January 2023

* *0.5 hours* finishing up ablation studies and determining optimal model configuration for 2d scans

### 18th January 2023

* *2 hours* updating inference script and preprocessing to allow for metric calculation on full sized weights and labels
* *0.5 hours* adjusting network and parameters to run on 3d scans again and beginning training run 

### 20th January 2023

* *3 hours* updating inference script and data loading to operate on unpreprocessed scans for correct metric computation and displaying of results. abstracting out inference methods to make building inference script easier

### 21st January 2023

* *11 hours* bug fixing in the inference script and updating model to work with slabs and multiple slabs (will require updating inference script again)

## Semester 2: Week 4

### 23rd January 2023

* *4 hours* using model trained overnight to correct inference script again. added per-organ dice, haussdorff distance, and means inference time computations to inference script

### 24th January 2023

* *5.5 hours* finished implementing metrics computations in inference script. got model inferencing and training on entire scans using checkpointing. begun work on getting the training to work on google colab.

### 27th January 2023

* *1 hour* updating data loading to load corect dataset for AMOS task 1. lowered slab size to allow for batch_size > 1 

### 29th January 2023

* *1 hour* adding logits overlapping to full scan processing

## Semester 2: Week 5

### 30th January 2023

* *4 hours* redownloading miccai dataset and making small adjustments to data loader to work better. expanded model to also take N slices of the logits before, i.e recusive scans. uploaded results to miccai, errors occured

### 31st January 2023

* *0.5 hours* experimenting with loss functions and retraining

### 4th February 2023

* *1 hour* beginning work on building docker image for second stage of AMOS submission

### 5th Febraury 2023

* *2.5 hours* finishing up docker image writing and testing

## Semester 2: Week 6

### 6th February 2023

* *1 hour* uploading docker image and adjusting model parameters (num_latents 512->1024, slab_depth 11->5, slaboverlap 5->2) for another training run

### 8th February 2023

* *0.25 hour* adjusting parameters for another training run (num_latent_channels 128->512, same changes as before as well)

### 9th February 2023

* *0.5 hours* advisor meeting 

## Semester 2: Week 6

### 13th February 2023

* *1 hour* began training run on full-scan 256x256 data after repreprocessing dataset 

### 15th February 2023

* *1 hour* began training run on less slabs but still 256x256 data as power cut caused other run to crash. emailed Dr. Gooya about what to do about full-sized 256x256 runs taking too long, meaning that  broadcasting/tiling results may not work and 256x256 runs may be infeasible on my home setup due to VRAM requirements

### 16th February 2023

* *4 hours* updating inference script to operate on selected slabs instead of always computing metrics and diffs for full scan. WIP

### 17th February 2023

* *4 hours* finalising slab-based update to inference script, was a silly mistake with how i was masking. preparing for a larger selected-slab training run again due to previously training it on background/all zeroes data

### 19th February 2023

* *7 hours* adding a new script and some adjustments to how parameters and fields are used in the inferences and model to allow for automated network parameter optimisation using a derivative-free optimisation library called nevergrad

## Semester 2: Week 7

### 20th February 2023

* *3 hours* updating limits for automated optimisation to prevent massive errors. Updating data loading to work from shared memory to improve efficiency. changed image precision to 32 bit and network precision to 16 bit, to save host and device memory

### 22nd February 2023

* *2 hours* further updates to automated optimisation script, starting larger run before weekly meeting

### 23rd February 2023

* *0.5 hours* advisor meeting

### 26th February 2023

* *1 hours* making optimiser pickle itself as PC crashed again, deleting two days of optimisations...
* *3 hours* writing introduction to dissertation

## Semester 2: Week 8

### 27th Febraury 2023

* *2 hours* writing background to dissertation

### 28th Febraury 2023

* *2 hours* writing background to dissertation
* *1 hour* writing documentation and preparing full scan training run

### 1st March 2023

* *4 hours* continuing with writing introduction

### 3rd March 2023

* *4 hours* finishing writing introduction

### 4th March 2023

* *3 hours* beginning and finishing requirements, begining writing design. changing how normalisation/standardisation works in data loader

### 5th March 2023

* *1 hour* severe issues present on home system after insatlling new ram. reset windows but issue persists during optimisation job. Have to make a docker container for the compute cluster

## Semester 2: Week 9

### 6th March 2023

* *2 hours* getting compute cluster working. made new docker image and sorted out data volumes

### 7th March 2023

* *4 hours* further attempts to debug system to no avail. creating training image and attempting to run optimisation on IDA compute cluster.

### 8th March 2023

* *4 hours* finished design section of report. further updates to docker images and ida compute cluster yaml configs to get them working. should be fully funcitonal now - bug was due to gpu memory not clearing which i cant guarantee sadly

### 10th March 2023

* *4 hours* wrting implementation section of report. more issues with compute cluster, have fixed to allow dp strategy for training the optimisation job

### 11th March 2023

* *2 hours* compute cluster volume has ran out of disk space. very very bad. no more network information can be stored, rending it unusable until storage increased. This is along with the finding that all the pods are running on the same machien, so i cannot realistically run all of the trainings at the same time. emails sent to gooya, dual boot installed on home system to try and get **somethign** trained for submission. will email about possible extension as i cannot control this

### 12th March 2023

* *2 hours* ran memtest86 on home system, uncovering numerous errors with new ram. removed said ram and attempting to train recursive on home system again. Restarted optimisation job to be better with the 32Gb of disk available on the volume. decreased scan size to give it a chance of finishing with enough time to train a full model

## Semester 2: Week 10

### 14th March 2023

* *2 hours* optimistaion job finished, optimised parameter full scan training started on cluster. several issues with getting it working so well see tomorrow. implementation section also finsihed. beginning future work section

### 15th March 2023

* *1 hours* full-scan inferencing failed. also starting up recursive and overlapping ablation tests with optimised parameters. should be easier to train. writing future work section as well

### 17th March 2023

* *3 hours* full-scan inferencing is hanging and randomly crashing. also seems that ablation studies are crashing likely due to some GPUs always having memory usage. closing a job also failed so having to wait to use the TITAN cards again. ablation only for now and have started a backup training on home system with reduced parameter sets. finished future work section, starting evaluation section and hoping that the results line up with what i think theyll be

### 18th March 2023

* *1 hours* looks like i dont register as a user on the compute cluster so it may be double allocating to other users while i try and use it, hopefully can work around by using a subset of the gpus and checking up on it. looks like full-scan training can be done on 3090s instead of titan cards so using them instead. Also more of them so maybe faster?

### 19th March 2023

* *2 hours* giving up on ablations on compute cluster, only home system with reduced parameters as nearly done. continuing with evaluation section and restarting jobs. stopped full-scan segmentation as not enough time to train it and a multi-modality one, so only training a partial optimised and partial multi-modality and full-scan multi-modality i reckon

## Semester 2: Week 11

### 20th March 2023

* *3 hours* partial optimised parameters job failed. ablation jobs are finsihed on home system so will just run multi-modality stuff on home system with reduced parameters instead of compute cluster cause its so flaky. will train to train a single optimised parameter full-scan multi-modality model on compute cluster since cant do optimised params on local. continuing with evaluation section and getting tables in to fill later. begun training partial multi-modality with reduced parameters on home system as backup

### 21st March 2023

* *3 hours* multi-modality on home system is thriving, compute cluster is dying. multi-modality on home system is done. running evaluations on all previous models before starting a backup run of the full-scan multi-modality baseline parameters on the home system.

### 23rd March 2023

* *.5 hours* supervisor meeting, sending current draft to hopefully get some feedback

### 25th March 2023

* *2 hours* writing evaluation section and including results. no longer checking compute cluster as home full-scan looks to be doing well and other results shiuld be enough

## Semester 2: Week 11

### 27th March 2023

* *.5 hours* stopping full-scan model trainign cause looks as though its converged. running more evaluations for evaluation section. evaluation section, bar a couple of results is done

### 28th March 2023

* *5 hours* running more evaluations. finsihed evaluation section except amos results submission. wrote conclusion. reworked future work chapter into a conclusion section instead. generated some images of segmentations for ghost classifications and examples. only got abstract, redraft, and presentation to do tomorrow and the day after then done a day early hopefully

### 29th March 2023

* *7 hours* trying to upload amos results, lots of errors. redrafted and looked over dissertation, added appendix with user manual, and written abstract

### 30th March 2023

* *6 hours* uploaded amos results finally and dsc score retrieved and included as final peice to dissertation. fully wrote presentation and script and saved to video, slightly speeding up to fit within 12 mins since at 14.5 atm. will upload when finished. finalising repository, adding dissertation and powerpoint.
