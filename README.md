# ParrotDenoiser: Parallel Estimation of Magnitude and Phase for High-Quality Speech Denoising

ParrotDenoiser is a time–frequency domain monaural speech enhancement model designed for high-quality noise reduction.  
Inspired by MP-SENet, it explicitly estimates both the magnitude and phase spectra in parallel, enabling cleaner and more intelligible speech in noisy environments.

A long-version of this architecture can also be extended to support speech dereverberation and bandwidth extension tasks.

Audio samples can be found at the demo website:  
[http://yxlu-0102.github.io/MP-SENet](http://yxlu-0102.github.io/MP-SENet)

We provide our open-source implementation in this repository.

## ⚠️ Note

There is a small bug inherited from the original code, which does **not** affect the model's overall performance.  
If you intend to retrain the model, it is **strongly recommended** to set `batch_first=True` in the `MultiHeadAttention` module inside `models/transformer.py`.  
This change significantly reduces memory usage.

## Pre-requisites

1. Python >= 3.6
2. Clone this repository
3. Install Python requirements:
   ```bash
   pip install -r requirements.txt
   ```

4. Download and extract the VoiceBank+DEMAND dataset:

   [https://datashare.ed.ac.uk/handle/10283/1942](https://datashare.ed.ac.uk/handle/10283/1942)
   Resample all `.wav` files to 16kHz, and organize the dataset as follows:

   ```
   VoiceBank+DEMAND/wavs_clean/
   VoiceBank+DEMAND/wavs_noisy/
   ```

   Alternatively, you may directly download the 16kHz version here:
   [Google Drive Link](https://drive.google.com/drive/folders/19I_thf6F396y5gZxLTxYIojZXC0Ywm8l)

## Training

To train the model using GPU(s):

```bash
CUDA_VISIBLE_DEVICES=0,1 python train.py --config config.json
```

Checkpoints and the configuration file are saved by default in the `cp_mpsenet` directory.
You can change the path using the `--checkpoint_path` option.

## Inference

```bash
python inference.py --checkpoint_file [generator checkpoint file path]
```

Pretrained checkpoint files are available in the `best_ckpt` directory.
To generate enhanced wav files:

```bash
python inference.py --checkpoint_file best_ckpt/g_best_vb --output_dir generated_files/ParrotDenoiser_VB
```

Output files are saved in `generated_files` by default. You can modify this using `--output_dir`.

## Model Structure

![Model Architecture](Figures/model.png)

## Comparison with Other SE Models

![Comparison Table](Figures/table.png)

## Acknowledgements

This work builds on concepts and codebases from:

- [HiFi-GAN](https://github.com/jik876/hifi-gan)
- [NSPP](https://github.com/YangAi520/NSPP)
- [CMGAN](https://github.com/ruizhecao96/CMGAN)

## Citation

If you reference this work, please also cite the original MP-SENet papers:

```bibtex

```