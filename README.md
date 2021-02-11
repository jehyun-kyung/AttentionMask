# Attribution Mask
Filtering Out Irrelevant Features By Recursively Focusing Attention on Inputs of DNNs

## Installation


### 1. Requirements
```bash
cd docker
```

### 2. Installaion of kaldi for speech
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

### 1. CIFAR-10
```bash
cd egs/xai/cifar10

# training
./run.sh --ngpu 4 --stage 1 --imgr_tag {tag_name}

# inference
./run.sh --ngpu 4 --stage 2 --imgr_tag {tag_name}
```

### 2. CIFAR-100
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