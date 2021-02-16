# Attribution Mask
Filtering Out Irrelevant Features By Recursively Focusing Attention on Inputs of DNNs

## Installation


### 1. Requirements
```bash
cd docker
```

### 2. Installaion of kaldi for espnet
```bash
git clone https://github.com/kaldi-asr/kaldi kaldi

cd kaldi/tools
extras/install_mkl.sh -s
extras/check_dependencies.sh
make -j 28
extras/install_irstlm.sh

cd ../src/
./configure
make depend -j 28
make -j 28
```

### 3. Installaion of espnet for input pipelines
```bash
cd tools

./meta_installers/install_espnet.sh
```

### 4. Installaion of hynet for customizing egs
```bash
cd tools

./meta_installers/install_hynet.sh
```

## Experiments
The default configurations for training and inference are written in ```conf/train.yaml``` and ```conf/decode.yaml``` respectively. 
### Example1. CIFAR-10

```bash
cd egs/xai/cifar10/conf/train.yaml
```

```yaml
dataset: cifar10
in_ch: 3
out_ch: 10

accum_grad: 1
max_epoch: 70
batch_size: 88

best_model_criterion:
-   - valid
    - acc_iter0
    - max
keep_nbest_models: 1

scheduler: multisteplr
scheduler_conf:
    milestones:
        - 60
    gamma: 0.1

optim: sgd
optim_conf:
    lr: 0.1
    weight_decay: 0.0005
    momentum: 0.9

xai_excute: 1
xai_mode: gxsi 
xai_iter: 3

bias: 0
batch_norm: 1
cfg_type: nib_D

# Studen-Teacher model related configurations
st_excute: 1  
teacher_cfg_type: nib_B2
teacher_model_path: exp/imgr_train_vgg7_bnwob/latest.pth
```

```bash
cd egs/xai/cifar10

# training
./run.sh --ngpu 4 --stage 1 --imgr_tag {tag_name}

# inference
./run.sh --ngpu 4 --stage 2 --imgr_tag {tag_name}
```

### Example2. CIFAR-100
```bash
cd egs/xai/cifar100

# training
./run.sh --ngpu 4 --stage 1 --imgr_tag {tag_name}

# inference
./run.sh --ngpu 4 --stage 2 --imgr_tag {tag_name}
```

## Reference

ESPNET : https://github.com/espnet/espnet

Neuron Merging: https://github.com/friendshipkim/neuron-merging
