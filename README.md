## Denoising Diffusion Probabilistic Models

An implementation of Denoising Diffusion Probabilistic Models for image generation written in PyTorch. This roughly follows the original code by Ho et al. Unlike their implementation, however, my model allows for class conditioning through bias in residual blocks. 

## Experiments

I have trained the model on MNIST and CIFAR-10 datasets. The model seemed to converge well on the MNIST dataset, producing realistic samples. However, I am yet to report the same CIFAR-10 quality that Ho. et al. provide in their paper. Here are the samples generated with a linear schedule after 2000 epochs:

![Samples after 2000 epochs](resources/samples_linear_200.png)

Here is a sample of a diffusion sequence on MNIST:

<p align="center">
  <img src="resources/diffusion_sequence_mnist.gif" />
</p>

### How to run

- Training:
```bash
python scripts/train_cifar.py
```

- Testing:
```bash
python scripts/sample_images.py
```

### Yuzhi's local computer example

- Environment:

1) pytorch 1.11.0, cudatoolkit 10.2

2) torchvision 0.12.0

3) wandb

- Preparation:

1) register an account on [wandb](https://wandb.ai/site)

2) login with that account

3) record the personal private API key, e.g., `44c0a5e96a4bae0dde739559a4e0e7035890ebb3` for my account `zhaoyuzhi987@gmail.com`

4) open a terminal on the local machine:
```bash
pip install wandb
wandb login (insert that API key)
```

5) create a new project, record the `project name`, e.g., `DDPM`

- Training:

1) insert the `project name` at line 150, e.g., `project_name="DDPM"`

2) comment the `entity` if the wandb account is private

3) change the log destination at line 142, e.g., `log_dir="./ddpm_logs"`:
```bash
mkdir ddpm_logs
```

4) run the example file:
```bash
python train_cifar.py
```

5) the training process uses approximately 9000Mb GPU memory, and the trained models will be automatically saved in `ddpm_logs` folder

## Resources

I gave a talk about diffusion models, NCSNs, and their applications in audio generation. The [slides are available here](resources/diffusion_models_talk_slides.pdf).

I also compiled a report with what are, in my opinion, the most crucial findings on the topic of denoising diffusion models. It is also [available in this repository](resources/diffusion_models_report.pdf).


## Acknowledgements

I used [Phil Wang's implementation](https://github.com/lucidrains/denoising-diffusion-pytorch) and [the official Tensorflow repo](https://github.com/hojonathanho/diffusion) as a reference for my work.

## Citations

```bibtex
@misc{ho2020denoising,
    title   = {Denoising Diffusion Probabilistic Models},
    author  = {Jonathan Ho and Ajay Jain and Pieter Abbeel},
    year    = {2020},
    eprint  = {2006.11239},
    archivePrefix = {arXiv},
    primaryClass = {cs.LG}
}
```

```bibtex
@inproceedings{anonymous2021improved,
    title   = {Improved Denoising Diffusion Probabilistic Models},
    author  = {Anonymous},
    booktitle = {Submitted to International Conference on Learning Representations},
    year    = {2021},
    url     = {https://openreview.net/forum?id=-NEXDKk8gZ},
    note    = {under review}
}
