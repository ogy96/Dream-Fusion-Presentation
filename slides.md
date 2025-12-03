---
theme: default
layout: cover
background: https://images.unsplash.com/photo-1581091012184-5c7361ce8a87?auto=format&fit=crop&w=1920&q=80
class: text-white
transition: fade
---

# **DreamFusion**

### **Text-to-3D Using 2D Diffusion**

ICLR 2023

**Ben Poole · Ajay Jain · Jonathan T. Barron · Ben Mildenhall**  
**Presented by: Ogün Yilmaz and Eren Güler**

<br>

🔗 **Paper:** https://arxiv.org/abs/2209.14988  
🔗 **GitHub Repo:** https://dreamfusion3d.github.io/

---

# 🚀 Motivation

- Creating 3D assets is **slow**, **expensive**, and requires expert tools
- AR/VR, gaming & simulation systems require **huge numbers** of assets
- 3D datasets are **small**, limiting generative modeling
- Meanwhile… **2D diffusion models exploded in quality**

---

# 💡 Core Question

> _Can we generate 3D objects from text using only a pretrained 2D diffusion model?_

DreamFusion answers: **YES — with zero 3D training data.**

---

# 🧠 Method Overview

## 🔍 High-Level Pipeline

1. Initialize a **Neural Radiance Field (NeRF)**
2. Render random camera views
3. Feed renders into a **frozen 2D diffusion model (Imagen)**
4. Compute **Score Distillation Sampling (SDS)** gradients
5. Update NeRF parameters
6. Repeat → A consistent 3D object forms

---

# 🖼 It works (OMG WOW!)

<video controls autoplay muted loop style="max-width: 100%; height: 80%;">
  <source src="https://dreamfusion-cdn.ajayj.com/sept28/wipe_opposite_6x4_smoothstep.mp4" type="video/mp4">
  Your browser does not support videos.
</video>

---

# 🎯 Core Innovation: SDS

## 🔑 Score Distillation Sampling (SDS)

- Uses a 2D diffusion model as a **frozen critic**
- Diffusion model outputs a **gradient direction** toward higher-likelihood images
- Avoids backprop through the entire diffusion U-Net
- Efficiently updates NeRF → consistent 3D geometry

✨ **Insight:** Teach NeRF to render images that the diffusion model "likes."

---

# 🧱 The 3D Representation (NeRF)

- Represents 3D scene as volume:
  - **density**
  - **albedo color**
- Additional components for stability & realism:
  - surface normals
  - random lighting
  - _textureless mode_ to force real geometry

🧠 **Trick:** Replace colors with white → prevents "painting over" geometry.

---

# 👁 View-Dependent Prompting

## Why We Need It

- Text prompts often assume a front view
- Training requires **multi-view consistency**

### Solution:

- "front view of…"
- "left side view of…"
- "back view…"
- "overhead view…"

This greatly stabilizes geometry.

---

# 🧪 Experiments

## Experimental Setup

### Datasets

- **Zero-shot**
- COCO captions for prompts
- No 3D dataset required

### Metrics

- **CLIP R-Precision**

### Baselines

- DreamFields
- CLIP-Mesh

### Ablations

- View augmentation
- Prompt rewriting
- Lighting
- Textureless rendering

---

# 🌟 Results

## Qualitative Results

DreamFusion generates:

- Clean 3D geometry
- Strong shape consistency
- Complex material structure
- High text alignment
- Multi-view coherence

Examples:

> "a bulldozer clearing snow"  
> "a lion reading a newspaper"  
> "a marble bust of a dragon"

---

# 🎬 Generated 3D Objects (DreamFusion)

### 🐿️ DSLR photo of a squirrel

<video controls autoplay muted loop style="max-width: 100%; border-radius: 12px;">
  <source src="https://dreamfusion-cdn.ajayj.com/journey_sept28/cropped/full_continuous/a_DSLR_photo_of_a_squirrel___rgbdn_hq_15000.mp4" type="video/mp4">
</video>

---

### 🐿️🐾 Squirrel wearing a kimono riding a motorcycle

<video controls autoplay muted loop style="max-width: 100%; border-radius: 12px;">
  <source src="https://dreamfusion-cdn.ajayj.com/journey_sept28/cropped/full_continuous/a_DSLR_photo_of_a_squirrel_wearing_a_kimono_riding_a_motorcycle_rgbdn_hq_15000.mp4" type="video/mp4">
</video>

## (Yes, we like squirrels!)

# Quantitative Highlights

**CLIP R-Precision**

- DreamFusion: **~79.7%**
- Outperforms DreamFields & CLIP-Mesh

**Textureless geometry metrics**

- Major improvement in geometric stability
- SDS produces more consistent multi-view geometry

✨ **Conclusion:** Best zero-shot text-to-3D model at time of publication.

---

# ⚠️ Limitations

## What DreamFusion Struggles With

- Imagen backbone is **64×64 → low detail**
- Optimization takes **1.5 hours per object**
- Geometry may collapse on flat surfaces
- Limited diversity
- Imagen is proprietary

---

# 🌍 Broader Impact

## Ethical & Societal Considerations

- Inherits **biases** from Imagen
- Can generate convincing **fake 3D assets**
- Automation concerns
- But also **democratizes 3D content creation**:
  - Education
  - Game prototyping
  - Rapid visualization

---

# 📚 Publication Details

## Paper Metadata

- **Conference:** ICLR 2023
- **Authors:** 4
- **Affiliation:** Google Research & UC Berkeley
- **Citations:** ~3,000+
- **Paper:** https://arxiv.org/abs/2209.14988
- **GitHub Slides:** https://dreamfusion3d.github.io/

---

# 💬 Personal Opinion

## What WE Liked

✔ Creative diffusion application  
✔ Zero-shot 3D from text  
✔ SDS is elegant + powerful  
✔ Visually impressive

## What WE Disliked

✘ Slow optimization  
✘ Low base resolution  
✘ Occasional unstable geometry  
✘ Imagen is closed-source

---

# **Thank You!**

## Any Questions?

🔗 **GitHub Repo:** https://dreamfusion3d.github.io/

🔗 **Paper:** https://arxiv.org/abs/2209.14988
