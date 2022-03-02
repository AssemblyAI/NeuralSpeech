## PriorGrad-vocoder

This repository is an official PyTorch implementation of the paper:

> Sang-gil Lee, Heeseung Kim, Chaehun Shin, Xu Tan, Chang Liu, Qi Meng, Tao Qin, Wei Chen, Sungroh Yoon, Tie-Yan Liu. "PriorGrad: Improving Conditional Denoising Diffusion Models with Data-Dependent Adaptive Prior." _ICLR_ (2022).
>[[arxiv]](https://arxiv.org/abs/2106.06406)
>

This repository contains a vocoder model (mel-spectrogram conditional waveform synthesis) presented in PriorGrad.

## Demo

Refer to the [demo page](https://speechresearch.github.io/priorgrad/) for the samples from the model.

## Quick Start and Examples

1. Navigate to PriorGrad-acoustic root and install dependencies
   ```bash
   # the codebase has been tested on PyTorch 1.8.2 LTS and 1.10.2 conda binaries
   pip install -r requirements.txt
   ```

2. Modify `filelists/train.txt`, `filelists/valid.txt`, `filelists/test.txt` so that the filelists point to the absolute path of the wav files. The codebase provides the LJSpeech dataset template. 

3. Train PriorGrad-vocoder 

   ```bash
   # the following command trains PriorGrad-vocoder with default parameters defined in params.py
   # need to specify model_dir, data_root, and training filelist
   python __main__.py \
   checkpoints/priorgrad \
   /path/to/your/LJSpeech-1.1 \
   filelists/train.txt
   ```

4. Inference (fast mode with T=6)
   ```bash
   # the following command performs test set inference of PriorGrad-vocoder with default parameters defined in params.py
   # inference requires the automatically generated params_saved.py during training, which is located at model_dir. 
   # need to specify model_dir, data_root, and test filelist
   python inference.py \
   checkpoints/priorgrad \
   /path/to/your/LJSpeech-1.1 \
   filelists/test.txt \
   --fast \
   --fast_iter 6
   ```
   
`--fast` `--fast_iter 6` uses fast inference noise schedule with `--fast-iter` reverse diffusion steps.

6, 12, and 50 `--fast_iter` are officially supported. If other value is provided, the model uses a linear beta schedule. Note that the linear schedule is expected to perform worse.

If `--fast` is not provided, the model performs slow sampling with the same `T` step forward diffusion used in training.

## Reference
If you find PriorGrad useful to your work, please consider citing the paper as below:

      @inproceedings{
      lee2022priorgrad,
      title={PriorGrad: Improving Conditional Denoising Diffusion Models with Data-Dependent Adaptive Prior},
      author={Lee, Sang-gil and Kim, Heeseung and Shin, Chaehun and Tan, Xu and Liu, Chang and Meng, Qi and Qin, Tao and Chen, Wei and Yoon, Sungroh and Liu, Tie-Yan},
      booktitle={International Conference on Learning Representations},
      year={2022},
      }

## Code of Conduct
This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct),
[trademark notice](https://docs.opensource.microsoft.com/releasing/), and [security reporting instructions](https://docs.opensource.microsoft.com/releasing/maintain/security/).