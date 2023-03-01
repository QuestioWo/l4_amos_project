# Readme

all code is contained within the perceiver-io submodule. Python library code is stored in the `perceiver/` directory. Model code is stored in the `perceiver/model/` directory, data loading code is stored in the `data/` directory, and misc. scripts for running different tests and activities can be found in the `scripts/` directory. In all of these cases, the majority of the developed and required code for the AMOS22 segmentations can be found in the `segmentation/` directories inside of each folder. The `docs/` directory contains documentation from the repository that the code was forked from. The `run_inference.py` script is also used by the `Dockerfile` for model inference service deployment.

## Build instructions

<!-- **You must** include the instructions necessary to build and deploy this project successfully. If appropriate, also include 
instructions to run automated tests.  -->

### Requirements

* Installation of Miniconda
* Running on Ubuntu 22.04 (development was completed on WSL but should not be necessary for running)

### Build steps

```bash
cd perceiver-io
conda env create -f environment.yml
conda activate perceiver-io
python -m pip install poetry -U
poetry install --all-extras
poetry build
```

### Test steps

To test that the code works, the model training can be ran from a fresh install. It does not require the `amos22/` dataset to run, however, it would help avoid errors.

```
conda activate perceiver-io
mkdir -p logs/miccai_seg
python -m perceiver.scripts.segmentation.mapper fit \
  --optimizer=AdamW \
  --optimizer.lr=5e-4 \
  --trainer.max_epochs=400 \
  --trainer.logger=TensorBoardLogger \
  --trainer.logger.save_dir=logs \
  --trainer.logger.name=miccai_seg \
  --data=MICCAIDataModule \
  --data.batch_size=1 \
  --data.dataset_dir=/path/to/amos22 \
  --trainer.log_every_n_steps=2 \
  --data.num_workers=8 \
  --trainer.check_val_every_n_epoch=1 \
  --trainer.accelerator=gpu \
  --trainer.devices=1
```

