# HiFi-VAEGAN
**English**  [简体中文](README_ZH.md)

## 0. Introduction
![Diagram](EnCodec.png)
**This network is equivalent to removing RVQ from the Encodec, please refer to the Encodec for the diagram. The training framework comes from [so-vits-svc](https://github.com/svc-develop-team/so-vits-svc).**

## 1. Install (recommended to use conda)
```
conda create -n hifi-vaegan python=3.10
```
```
conda activate hifi-vaegan
```
```
Install pytorch: https://pytorch.org/get-started/locally/
```
```
pip install -r requirements.txt
```

## 2. Prepare Data
You can use any high-quality audio data, including but not limited to vocals and instruments, and there is no need for classification.

Place all data in the "dataset_raw" folder without any nested subfolders.

## 3. Preprocessing
```
python resample.py
```

## 4. Modify config file
```
python preprocess_config.py
```
Then you can modify the following options as needed in the configs\config.json file

**log_interval:** Log interval recording, unit is step

**eval_interval:** Verification interval, unit is step

**learning_rate:** learning rate

**batch_size:** Increase it as much as possible to use all the video memory (Important!)

**fp16_run:** "False: is fp32, "True" uses **half_type** to control accuracy

**half_type:** Choose from bf16, fp16

**lr_decay:** The decay rate of the learning rate after each round

**segment_size:** Slice length, please find a balance between batch_size and this option

**keep_ckpts:** How many checkpoints to save

## 5. Train
```
python train.py -m <Experiment name>
```

## 6. Tensorboard
```
tensorboard --logdir=logs --load_fast=false
```