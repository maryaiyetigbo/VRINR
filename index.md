---
title: "Implicit Neural Representation for Video Restoration"
---


<!-- ✅ MathJax injection for LaTeX rendering -->
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

<!-- ✅ Add in your index.md just after the front matter `---` -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.3/font/bootstrap-icons.css" rel="stylesheet">


<style>
.link_button {
  display: inline-block;
  padding: 10px 16px;
  margin: 5px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border-radius: 6px;
  text-align: center;
  text-decoration: none;
}
.link_button:hover {
  background-color: #0056b3;
}
</style>


<center>

<h1>Implicit Neural Representation for Video Restoration</h1>

<!-- <h1 style="display: block;">Unsupervised Microscopy Video Denoising</h1> -->
<table style="border: none; display: initial;">
<tr style="border: none;">
<td style="border: none;"><a href="https://maryaiyetigbo.github.io/">Mary Damilola Aiyetigbo</a><sup>1</sup></td>
<td style="border: none;"><a href="mailto:wanqiy@clemson.edu">Wanqi Yuan</a></td>
<td style="border: none;"><a href="mailto:luofeng@clemson.edu">Feng Luo</a></td>
<td style="border: none;"><a href="mailto:nianyil@clemson.edu">Nianyi Li</a></td>
</tr>
</table>
<br>
<table style="border: none; display: initial;">
<tr style="border: none;">
<td style="border: none;">Clemson University</td>
<!-- <td style="border: none;"><sup>2</sup>MUSC</td> -->
</tr>
</table>

<br>

<table style="border: none; display: initial;">
<tr style="border: none;">
<td style="border: none;">
<a href="#" style="color: #ffffff">
<div class="link_button">
<i class="bi bi-file-earmark-richtext"></i> Paper
</div>
</a>
</td>
<td style="border: none; display: initial;">
<a href="https://github.com/maryaiyetigbo/VRINR" style="color: #ffffff">
<div class="link_button">
<i class="bi bi-github"></i> Code
</div>
</a>
</td>
</tr>
</table>

</center>


<!-- ## Two Photon Calcium Imaging
 <img src="./assets/highActivityb.gif" width="1000"/> -->

# Abstract

High-resolution (HR) videos play a crucial role in many computer vision applications.  Although existing video restoration (VR) methods can significantly enhance video quality by exploiting temporal information across video frames, they are typically trained for fixed upscalling factors and lack the flexibility to handle scales or degradations beyond their training distribution. In this paper, we introduce VR-INR, a novel video restoration approach based on Implicit Neural Representations (INRs) that is trained only on a single upscalling factor ($\times 4$) but generalizes effectively to arbitrary, unseen super-resolution scales at the test time. Notably, VR-INR also performs zero-shot denoising on noisy input, despite never having seen noisy data during training. Our methods employs a hierarchical spatial-temporal-texture encoding framework coupled with multi-resolution implicit hash encoding, enabling adaptive decoding of hight-resolution and noise-suppressed frames from low-resolution inputs at any desired magnification. Experimental results show that VR‑INR consistently maintains high-quality reconstructions at unseen scales and noise during training, significantly outperforming state‑of‑the‑art approaches in sharpness, detail preservation, and denoising efficacy.


## Architecture
<img src="./assets/pipeline.png" width="1000"/>

We propose **VR-INR**, a novel video restoration approach based on Implicit Neural Representations. VR-INR is trained only on clean data for super-resolution but generalizes effectively to arbitrary, unseen super-resolution scales at test time. Given an input sequence of low-resolution (LR) video: 
$$
\{\mathbf{I}^{\text{LR}}_{t}|t = 1, 2, \ldots, T\}
$$
 (where $$T$$ is the total number of frames, and 
$$
 \mathbf{I}^{\text{LR}}_{t}
$$
  represents a LR frame in the video) and a high-resolution grid 
$$
  \mathbf{r}^{\text{HR}}\in\mathbb{R}^2
$$
 specifying the spatial coordinates, VR-INR aims to produce high-resolution (HR) videos 
$$
\{\mathbf{I}^{\text{HR}}_{t}|t = 1, 2, \ldots, T\}
$$
. First, we employ hierarchical texture encoding network to extract and encode multi-scale local patches into spatial-temporal-texture feature representations $$\mathbf{F}_{\text{STT}}$$. For each target high-resolution coordinate 
$$
\mathbf{r}^{\text{HR}}
$$
 at frame 
$$
 t
$$, we retrieve a compact set of neighboring feature vectors from a spatial hash table using implicit hashing, and efficiently interpolate these vectors using adaptively learned weights to generate robust implicit features 
$$
\mathbf{v}^l
$$
. We then integrate these multi-resolution features $$\{\mathbf{v}^l\}_{l=1}^L$$ through a top-down attention mechanism, which sequentially refines and combines feature representations from coarse to fine resolutions. Finally, we decode the consolidated feature representations $$\mathbf{v}^{\text{HR}}$$ into RGB values using a multi-layer perceptron (MLP), generating the final HR video frames $$\mathbf{I}^{\text{HR}}_{t}$$.

## Results
<!-- Two Photon Calcium Imaging | Fluorescence Microscopy
:-------------------------:|:-------------------------:
<img src="./assets/standard.gif" width="400"/> | <img src="./assets/GOWT1.gif" width="400"/>

 Two Photon Calcium Imaging           |  Fluorescence Microscopy
:-------------------------:|:-------------------------:
![](./assets/standard.gif)  |  ![](./assets/GOWT1.gif) -->

<!-- ## Video SuperResolution -->
 <img src="./assets/suppl_Gopro.png" width="1000"/>

<!-- <table>
 <tr>
  <th align="center"> Two Photon Calcium Imaging </th>
  <th align="center"> Fluorescence Microscopy </th>
 </tr>
 <tr>
  <td align="center"> <img src="./assets/standard.gif" width="500"/> </td>
  <td align="center"> <img src="./assets/GOWT1.gif" width="500"/> </td>
 </tr>
</table> -->




<!-- ## Results on Natural Videos
<table style="border: none;">
 <tr style="border: none;"><th align="left" style="border: none;"> Bobblehead </th></tr>
 <tr style="border: none;"><td align="left" style="border: none;"> <img src="./assets/YTHFR_Gaussian50_bobblehead.gif" width="1000"/> </td></tr>
 <tr style="border: none;"><th align="left" style="border: none;"> Runner </th></tr>
 <tr style="border: none;"><td align="left" style="border: none;"> <img src="./assets/YTHFR_Gaussian50_1Runner.gif" width="1000"/> </td></tr>
</table> -->


 <!-- Bobblehead           |  Runner
:-------------------------:|:-------------------------:
![](./assets/YTHFR_Gaussian50_bobblehead.gif)  |  ![](./assets/YTHFR_Gaussian50_1Runner.gif) --> -->

<!-- ###
![result](./assets/results.png) -->

<!-- **Performance in Denoising Synthetic Noise.** This table presents a comparison of average PSNR/SSIM values of denoised performance on LIVE-YT-HFR datasets on different noise types and intensities. Our method demonstrates superior performance in most cases and remains highly competitive with the supervised methods.