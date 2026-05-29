# CogFlow Public Release

This release focuses on the public CogFlow training and evaluation pipeline for two datasets:

- `rat`
- `babel`

## What Is Included

Three public presets are supported:

1. `rat`: standard rat training and evaluation
2. `babel`: standard babel training and evaluation

The recommended public entry points are:

- `train.py`
- `eval.py`
- `pub_evaluation.py`

## Environment

```bash
conda create -n cogsde python=3.11 -y
conda activate cogsde
pip install -r requirements.txt
```

Install a PyTorch build that matches your CUDA runtime before running training or evaluation.

## Data And Weights

Download the public dataset packages and weight packages from: 
```link
https://drive.google.com/drive/folders/1yxv7f1Kbmaj-isupohGRdxznwEulZx0G?usp=sharing
```

then place them in the following locations.

### Rat dataset

Expected files:

```text
data/rat/rat_pose_train.npy
data/rat/rat_stim_train.npy
data/rat/rat_pose_val.npy
data/rat/rat_stim_val.npy
```

Optional aliases also supported for evaluation:

```text
data/rat/rat_pose_test.npy
data/rat/rat_stim_test.npy
```

### Babel dataset

Expected files:

```text
data/babel/babel_train.npy
data/babel/babel_train_cmd.npy
data/babel/babel_val.npy
data/babel/babel_val_cmd.npy
data/babel/babel_test.npy
data/babel/babel_test_cmd.npy
```

### Public checkpoints

Place downloaded checkpoints here:

```text
results_rat/cor_rat_fm_mn_std/m3_drift_diffusion/models/checkpoint_best.pt
results_babel/cor_babel_fm_m1_std/m3_drift_diffusion/models/checkpoint_best.pt
```

## Train

### Default rat

```bash
python train.py --cfg cfg/full_cfg/cor_rat_fm_mn.yml --exp rat_release
```

If $L_{\textrm{bnd}}$ is included, use the following command:
```bash
python train.py --cfg cfg/full_cfg/cor_rat_fm_mn.yml --exp rat_test --enable_dissipativity --dissipativity_weight 0.001
```

### Default babel

```bash
python train.py --cfg cfg/full_cfg/cor_babel_fm_m1.yml --exp babel_release
```

## Evaluate

### Generic evaluation

```bash
python eval.py --cfg cfg/full_cfg/cor_rat_eval_mn.yml 
python eval.py --cfg cfg/full_cfg/cor_babel_fm_m1.yml
```

## Public Evaluation

`pub_evaluation.py` is a quick validation to reproduce the released evaluation presets.

### Default rat

```bash
python pub_evaluation.py --npz_path cfg/full_cfg/npz/rat_cogflow.npz
```

### Default babel

```bash
python pub_evaluation.py --npz_path cfg/full_cfg/npz/babel_cogflow.npz
```
