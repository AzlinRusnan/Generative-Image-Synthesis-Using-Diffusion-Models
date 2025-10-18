# Reproducing Figures from Denoising Diffusion Probabilistic Models (DDPM)

This project reproduces the **visual figures** from the paper:
*Jonathan Ho, Ajay Jain, Pieter Abbeel (NeurIPS 2020)*  
[Paper Link](https://arxiv.org/abs/2006.11239)

The paper introduced a new class of **generative models** called **Diffusion Probabilistic Models (DDPMs)** — models that generate realistic images by **gradually denoising random Gaussian noise**.  

Because the original implementation relies on **TensorFlow 1.x** and **TPUs**, this project focuses on **reproducing the visual results** using **modern PyTorch-based tools** from Hugging Face’s `diffusers` library.

---

## Understanding the Paper

### What is a Diffusion Model?

Diffusion models generate data (like images) by reversing a *gradual noise process*.

1. **Forward process (Diffusion):**  
   Start from a real image `x₀`, and repeatedly add small Gaussian noise until it becomes random noise `x_T`.

2. **Reverse process (Denoising):**  
   Train a neural network to reverse this process — step by step — predicting and removing the noise added earlier.

3. **Sampling:**  
   At inference time, the model starts from pure noise and denoises it repeatedly to create a realistic image.


### Why It’s Important
- DDPMs can produce **high-quality**, **stable**, and **diverse** samples — comparable to GANs but easier to train.
- The model’s iterative denoising process is the foundation for later models like **DDIM**, **Stable Diffusion**, and **Imagen**.

---

## Project Goal

The goal is to **reproduce the paper’s figures** (sample images) using **publicly available pretrained DDPM models**, while staying as close as possible to the original experimental setup — within the limitations of Google Colab.

---

## Implementation Overview

| Dataset | Model Used | Image Size | Steps | Notes |
|----------|-------------|-------------|--------|--------|
| CIFAR-10 | `google/ddpm-cifar10-32` | 32×32 | 1000 | Closely follows the paper setup |
| LSUN Bedroom | `google/ddpm-bedroom-256` | 256×256 | 250 | Reduced from 1000 for runtime |
| LSUN Church | `google/ddpm-church-256` | 256×256 | 250 | Balanced quality vs speed |
| CelebA-HQ | `CompVis/stable-diffusion-v1-4` | 256×256 | — | Substituted Stable Diffusion to simulate DDPM face samples |

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
- Needed custom data pipelines.

To make reproduction feasible:
- Used **PyTorch + Hugging Face Diffusers** (modern, simple).
- Used **pretrained models** instead of training from scratch.
- Substituted **Stable Diffusion** for CelebA-HQ since both share the same diffusion foundation.

These adaptations maintain the **concept and visual fidelity** of the original work while making it runnable on Colab.

---


