## Reproducing Figures from Denoising Diffusion Probabilistic Models (DDPM)

This project reproduces the **visual figures** from the paper:

**Denoising Diffusion Probabilistic Models**  
*Jonathan Ho, Ajay Jain, Pieter Abbeel (NeurIPS 2020)*  
[Paper Link](https://arxiv.org/abs/2006.11239)

---

## About Generative AI

**Generative Artificial Intelligence (GenAI)** refers to models that can *create* new data such as images, text, music, or video that resembles real-world examples.  

Instead of just recognizing or sorting data, generative models learn what the data usually looks like its patterns and structure and use that knowledge to create new, realistic examples.

Common families of GenAI models include:
- **GANs (Generative Adversarial Networks):** two networks compete — one generates, one discriminates.  
- **VAEs (Variational Autoencoders):** learn a latent representation to reconstruct and generate data.  
- **Autoregressive Models:** generate data one element (e.g., pixel or token) at a time.  
- **Diffusion Models:** generate data by gradually **denoising random noise**, producing clean, detailed outputs.

Diffusion models now form the backbone of modern image generators such as **Stable Diffusion**, **DALL·E 2**, and **Imagen**, offering a balance of **high quality**, **training stability**, and **controllable generation**.

---

## Understanding the Paper

The paper introduced **Diffusion Probabilistic Models (DDPMs)**, a class of generative models that **learn to reverse a noise-adding process** to generate realistic images from pure noise.  

Because the original implementation relied on **TensorFlow 1.x** and **TPUs**, this project focuses on **reproducing the visual results** using **modern PyTorch-based tools** from Hugging Face’s `diffusers` library.

### How DDPM Works?

1. **Forward process (Diffusion):**  
   Start from a real image `x₀`, and repeatedly add small Gaussian noise until it becomes random noise `x_T`.

2. **Reverse process (Denoising):**  
   A neural network is trained to *undo* this process — step by step — predicting and removing noise to recover the image.

3. **Sampling:**  
   At inference, the model starts from random noise and applies the learned denoising steps to generate a clean image.


### Why It’s Important
- DDPMs can produce **high-quality**, **stable**, and **diverse** samples, comparable to GANs but easier to train.
- The model’s iterative denoising process is the foundation for later models like **DDIM**, **Stable Diffusion**, and **Imagen**.

---

## Project Goal

The goal is to **reproduce the paper’s figures** (sample images) using **publicly available pretrained DDPM models**, while staying as close as possible to the original experimental setup — within the limitations of Google Colab.

---

## What I Did

1. Used **pretrained DDPM models** from Hugging Face’s `diffusers` library.
2. Generated **CIFAR-10** (32×32) and **LSUN** (256×256) samples similar to those in the paper.
3. Replaced the original **CelebA-HQ DDPM** with **Stable Diffusion** (for practical reasons) to produce face-like images.
4. Experimented with **different inference step counts** (1000 vs 250) to trade off image quality vs runtime.
5. Managed **GPU memory cleanup** between runs to prevent Colab crashes.
6. Collected, organized, and visualized generated samples to match the paper’s figures.

---

##  Why Substitutions Were Made

The **original DDPM setup**:
- Used TensorFlow 1.x,
- Trained on TPUs with massive compute requirements,
- Required complex data pipelines.

To make reproduction feasible:
- Used **PyTorch + Hugging Face Diffusers** (modern, simple).
- Used **pretrained models** instead of retraining.  
- Substituted **Stable Diffusion** for CelebA-HQ since both share the same diffusion foundation.

These adaptations maintain the **concept and visual fidelity** of the original work while making it runnable on Colab.

## Results

### CelebA-HQ (via Stable Diffusion)
Simulated CelebA-HQ-like face images using **Stable Diffusion v1-4**.

![CelebA HQ Samples](https://github.com/AzlinRusnan/Generative-Image-Synthesis-Using-Diffusion-Models/blob/main/Images/celeb.jpg)

---

### CIFAR-10 Samples (32×32)
Generated using pretrained `google/ddpm-cifar10-32` with **1000 denoising steps**.

![CIFAR-10 Samples](https://github.com/AzlinRusnan/Generative-Image-Synthesis-Using-Diffusion-Models/blob/main/Images/cifar.jpg)

---

### LSUN Bedroom Samples (256×256)
Generated using pretrained `google/ddpm-bedroom-256` with **250 denoising steps**.

![LSUN Bedroom Samples](https://github.com/AzlinRusnan/Generative-Image-Synthesis-Using-Diffusion-Models/blob/main/Images/lsunb.jpg)

---

### LSUN Church Samples (256×256)
Generated using pretrained `google/ddpm-church-256` with **250 denoising steps**.

![LSUN Church Samples](https://github.com/AzlinRusnan/Generative-Image-Synthesis-Using-Diffusion-Models/blob/main/Images/lsunc.png)

---
## Results Summary

| Dataset | My Setup | Visual Quality | Notes |
|----------|-------------|-------------|--------|
| CelebA-HQ | Stable Diffusion | Excellent | Substitute for face samples |
| CIFAR-10 | 1000 | Good | Matches paper’s denoising process|
| LSUN Bedroom | 250 | Good | Slightly softer textures |
| LSUN Church | 250 | Good | Preserves structural details |

---
## What I Learned

- Reproducing research papers often requires **engineering trade-offs** due to compute and framework constraints.  
- **Hugging Face Diffusers** makes diffusion model experimentation practical and accessible.  
- Understanding the **denoising principle** helps in adapting newer diffusion architectures.  
- Reducing inference steps (e.g., 1000 → 250) offers a good balance between runtime and image fidelity.  

---

