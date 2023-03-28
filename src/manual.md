# User manual 

<!-- Describe how to use your software, if this makes sense for your code. Almost all projects should have at least some instructions on how to run the code. More extensive instructions can be provided here. -->

## Development

### Prerequisites

* Miniconda installed
* Running on Ubuntu 22.04 (development was completed on WSL but should not be necessary for running)
* [`amos22` dataset](https://zenodo.org/record/7155725#.Y_7WqHbP1D-) stored somewhere. where the path is important, it will be noted.

### Creating environment

This is required for all further steps, which all assume that the conda `perceiver-io` environment is activated already

```bash
cd perceiver-io
conda env create -f environment.yml
conda activate perceiver-io
python -m pip install poetry -U
poetry install --all-extras
poetry build
```

### Preprocessing dataset

This will run automatically when the dataset is loaded, but can be ran individually as well. It assumes that the dataset can be found at `/mnt/d/amos22`, this must be changed inside of `perceiver/scripts/segmentation/preproc.py` if not true:

```bash
cd perceiver-io
sh scripts/miccai/preproc.sh
```

### Running training

```bash
cd perceiver-io
cp -r /path/to/amos22 /dev/shm # load amos22 dataset into shared memory. not all data must be loaded to memory, only, imagesTr_preprocessed/* labelsTr_preprocessed/*, dataset.json, and several empty folders: [imagesTr, imagesVa, imagesVa_preprocessed, labelsTr, labelsVa, labelsVa_preprocessed]
sh scripts/miccai/train.sh
```

### Running inference

```bash
cd perceiver-io
cp -r /path/to/amos22 /dev/shm # load amos22 dataset into shared memory. not all data must be loaded to memory, only, imagesTr_preprocessed/* labelsTr_preprocessed/*, dataset.json, and several empty folders: [imagesTr, imagesVa, imagesVa_preprocessed, labelsTr, labelsVa, labelsVa_preprocessed] This obviously depends on what dataset split is to be inferenced
python -m perceiver.scripts.segmentation.inference # several configuration parameters can be changed in the GLOBALS at the start of the corresponding file
```

### Running automated parameter optimisation

```bash
cd perceiver-io
cp -r /path/to/amos22 /dev/shm # load amos22 dataset into shared memory. not all data must be loaded to memory, only, imagesTr_preprocessed/* labelsTr_preprocessed/*, dataset.json, and several empty folders: [imagesTr, imagesVa, imagesVa_preprocessed, labelsTr, labelsVa, labelsVa_preprocessed]
sh scripts/miccai/automated_optimise.sh 2>&1 | tee log.txt # optimal parameters will be printed to the console, hence recommending using the use of tee
```

## Docker deployment

### Prerequisite

* docker installed
* trained model weights
* image used for coregistration (normally found in `amos22/imagesTr_preprocessed/coregistration_image.nii.gz`)

### Building image

```bash
cd perceiver-io
sh scripts/docker_build.sh path/to/model.ckpt path/to/coregistration_image.nii.gz tagname
```

### Deploying/pushing iamge

```bash
docker push tagname
```

### Using docker image for inference

There is already a prebuilt docker image deployed on ghcr.io. It can be pulled using:

```bash
docker pull ghcr.io/questiowo/miccai-perceiver-io
```

This may require logging in, [information on how to do so can be found in GitHub documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-with-a-personal-access-token-classic)

Information on how to correctly run the docker image using GPU acceleration can be found in [the AMOS22 docker submission guidelines here](https://github.com/JiYuanFeng/AMOS/tree/docker#step-4-run-a-container-from-a-created-docker-image)

### Using OpenShift Compute Cluster

The OpenShift compute cluster GPUs can be used to train on by using the associated `Dockerfile.XXX` docker image. These are currently uploaded, ready for use on [hub.docker.com](https://hub.docker.com/search?q=perceiver-io).

The configuration yaml files are included in the project as `job-perceiver-io-*.yaml`. The jobs expect the `amos22` dataset to be uploaded to an associated NFS store, which can be attached at `/volume/`. This is configured in the yaml-file and can be adjusted to new users easily.

The docker commands are written into each Dockerfile and are not observant to different numbers of GPGPUs. This means that if a cluster with (not 2) GPUs is available, the docker image has to be rebuilt, repushed, and the job restarted with the correct batch size and devices. Alternatively, the yaml configuration files can be extended to instead have the training job script inside the configuration file instead of the Dockerfile, however, an example is not included of that.