<h1 align="center">FigStep: Jailbreaking Large Vision-language Models via Typographic Visual Prompts</h1>

<p align='center' style="text-align:center;font-size:1em;">
Yichen Gong, Delong Ran, Jinyuan Liu, Conglei Wang, <a href="https://tianshuocong.github.io/" target="_blank" style="text-decoration: none;">Tianshuo Cong</a>, <a href="mailto: anyuwang@tsinghua.edu.cn" target="_blank" style="text-decoration: none;">Anyu Wang</a>, Sisi Duan, Xiaoyun Wang  
</p>

$${\color{red}\text{\textbf{Warning: This repo contains harmful model responses!!!}}}$$

[![arXiv](https://img.shields.io/badge/arxiv-2311.05608-b31b1b)](https://arxiv.org/abs/2311.05608) ![GitHub Repo stars](https://img.shields.io/github/stars/ThuCCSLab/FigStep) ![GitHub watchers](https://img.shields.io/github/watchers/ThuCCSLab/FigStep)

<div align="center">
<img width="50%" alt="FigStep" src="assets/figstep.jpg">
</div>

$${\color{gray}\text{\emph{ The figure, created by DALL·E 3, is inspired by and serves as a tribute to the film ``The Shawshank Redemption.''}}}$$

## Overview
FigStep is a black-box, no gradient needed jailbreaking algorithm against large vision-language models (VLMs).
For instance, FigStep feeds harmful instructions into VLMs through the image channel and then uses benign text prompts to induce VLMs to output contents that violate common AI safety policies.
Our experimental results reveal that VLMs are vulnerable to jailbreaking attacks, which highlights the necessity of novel safety alignments between visual and textual modalities

<div align="center">
<img width="80%" alt="FigStep" src="assets/workflow.png">
</div>

## Usage
To bypass the safety alignment in the textual module of VLM, FigStep should embed
harmful information into image-prompts, where typographing is the most direct approach. Therefore, FigStep leverages the screenshot of the post-paraphrase instruction as the final malicious image-prompt. Please import the code in `src/generate_prompts.py` to generate such text-screenshots.
 

## Dataset
We release `SafeBench`, a dataset of 500 questions on 10 topics that are forbidden by both OpenAI and Meta usage policies.
Please see `data/question/safebench.csv` for more details.
The harmful questions are generated by GPT-4.
We used `Prompt 3` in our paper to generate these harmful questions.

## Results
The harmfulness score (evaluated by GPT-4 evaluator) distribution for FigStep attack demonstrates a similar pattern among different open-source models (LLaVA and MiniGPT-4), exhibiting pronounced peaks at a score of 5, with minimal occurrences at other scores.

<div align="center">
<img width="100%" alt="FigStep" src="assets/asr.png">
</div>

Also, FigStep can achieve high ASR across different VLMs and different harmful topics.

<div align="center">
<img width="100%" alt="FigStep" src="assets/asr_topic.png">
</div>

To examine how FigStep affects the model’s behavior, we generate different
prompts for the same query and compare their semantic embeddings.
The results in the following figure reveal that the embeddings of benign and harmful queries are clearly separated when using `Prompt 6` in our paper, suggesting that the underlying LLM can distinguish them well. However, the embeddings of benign and harmful queries are blended together when using FigStep, suggesting that the visual modality is not safely aligned.

<div align="center">
<img width="50%" alt="FigStep" src="assets/tsne.png">
</div>


## FigStep-Pro
We noticed that OpenAI launched an OCR tool to detect the presence of harmful
information with the image-prompt. 
However, we find that an upgraded version of FigStep, namely `FigStep-Pro`, could bypass the OCR detector and then jailbreak GPT-4V.
Compared with FigStep, FigStep-Pro leverages additional post-processing: FigStepPro cuts up the screenshot of FigStep (see Figure 12). To this end, the text in each sub-figure is then turned harmless or meaningless and passes the moderation test. Then we feed all the subfigures together into GPT-4V and design an inciting text-prompt to induce GPT-4V to concatenate subfigures and generate the steps to manufacture the item with the concatenated image.


## Jailbreak Instances
<div align="center">
<img width="100%" alt="FigStep" src="assets/instance.png">
</div>



## Citation

If you find our work helpful, please star us 🌟 and cite it as follows:
```bibtex
@misc{gong2023figstep,
      title={FigStep: Jailbreaking Large Vision-language Models via Typographic Visual Prompts}, 
      author={Yichen Gong and Delong Ran and Jinyuan Liu and Conglei Wang and Tianshuo Cong and Anyu Wang and Sisi Duan and Xiaoyun Wang},
      year={2023},
      eprint={2311.05608},
      archivePrefix={arXiv},
      primaryClass={cs.CR}
}
```
