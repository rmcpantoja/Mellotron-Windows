![Mellotron](mellotron_logo.png "Mellotron")

### Rafael Valle\*, Jason Li\*, Ryan Prenger and Bryan Catanzaro
In our recent [paper] we propose Mellotron: a multispeaker voice synthesis model
based on Tacotron 2 GST that can make a voice emote and sing without emotive or
singing training data. 

By explicitly conditioning on rhythm and continuous pitch
contours from an audio signal or music score, Mellotron is able to generate
speech in a variety of styles ranging from read speech to expressive speech,
from slow drawls to rap and from monotonous voice to singing voice.

Visit our [website] for audio samples.

## Pre-requisites
1. NVIDIA GPU + CUDA cuDNN

## Setup
1. Clone this repo: `git clone https://github.com/NVIDIA/mellotron.git` (Install Git for Windows): [Download](https://git-scm.com/download/win)
2. CD into this repo: `cd mellotron`
3. Initialize submodule: `git submodule init; git submodule update`
4. Install Anaconda: [Download](https://www.anaconda.com/products/individual)
5. conda create -n mellotron python=3.8
6. conda activate mellotron
7. Install conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch
8. Install [Apex]
9. Install python requirements or build docker image 
    - Install python requirements: `pip install -r requirements.txt`

## Training
1. Update the filelists inside the filelists folder to point to your data
2. `python train.py --output_directory=outdir --log_directory=logdir`
3. (OPTIONAL) `tensorboard --logdir=outdir/logdir`

## Training using a pre-trained model
Training using a pre-trained model can lead to faster convergence  
By default, the speaker embedding layer is [ignored]

1. Download our published Mellotron model trained on [LibriTTS] or [LJS]
2. `python train.py --output_directory=outdir --log_directory=logdir -c models/mellotron_libritts.pt --warm_start`

## Multi-GPU (distributed) and Automatic Mixed Precision Training
1. `python -m multiproc train.py --output_directory=outdir --log_directory=logdir --hparams=distributed_run=True,fp16_run=True`

## Inference demo
1. `jupyter notebook --ip=127.0.0.1 --port=31337`
2. Load inference.ipynb 
3. (optional) Download our published [WaveGlow](https://drive.google.com/open?id=1okuUstGoBe_qZ4qUEF8CcwEugHP7GM_b) model

## Related repos
[WaveGlow](https://github.com/NVIDIA/WaveGlow) Faster than real time Flow-based
Generative Network for Speech Synthesis.

## Acknowledgements
This implementation uses code from the following repos: [Keith
Ito](https://github.com/keithito/tacotron/), [Prem
Seetharaman](https://github.com/pseeth/pytorch-stft), 
[Chengqi Deng](https://github.com/KinglittleQ/GST-Tacotron),
[Patrice Guyot](https://github.com/patriceguyot/Yin), as described in our code.

[ignored]: https://github.com/NVIDIA/mellotron/blob/master/hparams.py#L22
[paper]: https://arxiv.org/abs/1910.11997
[WaveGlow]: https://drive.google.com/open?id=1rpK8CzAAirq9sWZhe9nlfvxMF1dRgFbF
[LibriTTS]: https://drive.google.com/open?id=1ZesPPyRRKloltRIuRnGZ2LIUEuMSVjkI
[LJS]: https://drive.google.com/open?id=1UwDARlUl8JvB2xSuyMFHFsIWELVpgQD4
[pytorch]: https://github.com/pytorch/pytorch#installation
[website]: https://nv-adlr.github.io/Mellotron
[Apex]: https://github.com/nvidia/apex
[AMP]: https://github.com/NVIDIA/apex/tree/master/apex/amp
