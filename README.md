<div align="center">
<img src='assets/logo_long.png' style="height:60px"></img>
</div>
<h1 align="center">
 [ICLR 2025 Oral] <i>Open-World Reinforcement Learning over Long Short-Term Imagination</i> </h1>
<!--  <img src="./assets/minecraft.png" alt="logo" style="width: 32px; height: 32px; margin-right: 7px; margin-bottom: 0px;"> -->
<p align="center">
    Jiajian Li*
    ·
    Qi Wang*
    ·
    Yunbo Wang
    ·
    Xin Jin
    ·
    Yang Li
    ·
    Wenjun Zeng
    ·
    Xiaokang Yang
  </p>

<h3 align="center"> <a href="https://openreview.net/pdf?id=vzItLaEoDa" target="_blank"> Paper </a> &nbsp;&nbsp; |&nbsp;&nbsp;   <a href="https://arxiv.org/pdf/2410.03618" target="_blank"> arXiv </a> &nbsp;&nbsp; | &nbsp;&nbsp; <a href="https://qiwang067.github.io/ls-imagine" target="_blank"> Website </a> &nbsp;&nbsp; </h3>
  <div align="center"></div>
<p align="center">
  <a href="#quick-start"><b>⚡ Quick Start</b></a> |
  <a href="#pretrained-weights"><b>📥 Checkpoints Download</b></a> |
  <a href="#citation"><b>📝 Citation</b></a> <br>
</p>

<p align="center">
<img src="assets/overview.png" alt="Teaser image" />
</p>

<p style="text-align:justify">
  Training visual reinforcement learning agents in a high-dimensional open world presents significant challenges. While various model-based methods have improved sample efficiency by learning interactive world models, these agents tend to be "short-sighted", as they are typically trained on short snippets of imagined experiences. We argue that the primary challenge in open-world decision-making is improving the exploration efficiency across a vast state space, especially for tasks that demand consideration of long-horizon payoffs. In this paper, we present LS-Imgine, which extends the imagination horizon within a limited number of state transition steps, enabling the agent to explore behaviors that potentially lead to promising long-term feedback. The foundation of our approach is to build a <i>long short-term world model</i>. To achieve this, we simulate goal-conditioned jumpy state transitions and compute corresponding affordance maps by zooming in on specific areas within single images. This facilitates the integration of direct long-term values into behavior learning. Our method demonstrates significant improvements over state-of-the-art techniques in MineDojo.
</p>

## Showcases
<table style="margin: auto;">
<table class="center">
  <tr>
    <td align="center">Harvest log in plains</td>
    <td align="center">Harvest water with bucket</td>
    <td align="center">Shear sheep</td>
    <td align="center">Mine iron ore</td>
  </tr>
  <tr>
    <td>
      <img src="assets/iron_demo.gif" width="170">
    </td>
    <td>
      <img src="assets/log_demo.gif" width="170">
    </td>
    <td>
      <img src="assets/water_demo.gif" width="170">
    </td>
    <td>
      <img src="assets/wool_demo.gif" width="170">
    </td>
  </tr>
</table>
<img src="assets/success_rate_with_barplot.png" alt="evaluation_results" width="90%"/>

<!-- 
<p align="center">
</p>
# Open-World Reinforcement Learning over Long Short-Term Imagination

#### Open-World Reinforcement Learning over Long Short-Term Imagination

Jiajian Li*, Qi Wang*, Yunbo Wang, Xin Jin, Yang Li, Wenjun Zeng, Xiaokang Yang

[[arXiv]](https://arxiv.org/pdf/2410.03618)  [[Project Page]](https://qiwang067.github.io/ls-imagine) -->

## Quick Start
### Install the Environment
LS-Imagine is implemented and tested on Ubuntu 20.04 with python==3.9:

1. Create an environment
    ```bash
    conda create -n ls_imagine python=3.9
    conda activate ls_imagine 
    ```

2. Install Java: JDK `1.8.0_171`. Then install the [MineDojo](https://github.com/MineDojo/MineDojo) environment and [MineCLIP](https://github.com/MineDojo/MineCLIP) following their official documents. During the installation of MineDojo, various errors may occur.

> [!IMPORTANT]
>**We provide the detailed installation process and solutions to common errors, please refer to [here](./docs/minedojo_installation.md).**

4. Install dependencies
    ```bash
    pip install -r requirements.txt
    ```

5. Download the MineCLIP weight [here](https://drive.google.com/file/d/1uaZM1ZLBz2dZWcn85rZmjP7LV6Sg5PZW/view?usp=sharing) and place them at `./weights/mineclip_attn.pth`.

6. We provide two options for recording data during the training process: TensorBoard and Weights & Biases (wandb). 

   - To use TensorBoard, set `use_wandb` to `False` in the `./config.yaml` file.
   - To use wandb (optional), set `use_wandb` to `True` in the `./config.yaml` file. Additionally, retrieve your wandb API key and set it in the `./config.yaml` file under the field `wandb_key: {your_wandb_api_key}`.


### Pretrained Weights

We provide pretrained weights of **LS-Imagine** for the tasks mentioned in the paper. You can download them using the links in the table below and rename the downloaded file to `latest.pt`:

<div align="center">

| Task Name                  | Weight File                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------|
| harvest_log_in_plains      | [latest_log.pt](https://drive.google.com/file/d/1_mhz49YPJDMNmPB-WwbzCG6zCTUidFQ3/view?usp=drive_link)                                                                |
| harvest_water_with_bucket  | [latest_water.pt](https://drive.google.com/file/d/1DxtQ-ZckTVw1tFySspKRaxoaShDi_b8A/view?usp=drive_link)                                                              |
| harvest_sand               | [latest_sand.pt](https://drive.google.com/file/d/1xa6JwV7rh-IfGoFjWDoneWpaTwPxLWb_/view?usp=drive_link)                                                               |
| mine_iron_ore              | [latest_iron.pt](https://drive.google.com/file/d/1FOIRGQJvgeQptK8-4cVVGv_jeNIy8kw7/view?usp=drive_link)                                                               |
| shear_sheep                | [latest_wool.pt](https://drive.google.com/file/d/1sx7IVOZ1JYs0BJHD3TWZcPb-f-x5xfA3/view?usp=drive_link)                                                               |

</div>

<a name="evaluation_with_checkpoints"></a>
To start a evaluating run from one of these checkpoints:

1. Set up the task for evaluation ([instructions here](./docs/task_setups.md)).

2. Run the following command to test the success rate:
    ```bash
    sh ./scripts/test.sh /path/to/latest.pt 100 test_harvest_log_in_plains
    ```

<!-- 5. Download the Multimodal U-Net weight [here](https://drive.google.com/file/d/1Ylhw-MkT1UIUX5EyOosNmF09bWSlEjSf/view?usp=sharing), rename it to `swin_unet_checkpoint.pth`, place it at `finetune_unet/finetune_checkpoints/harvest_wool_in_plains` -->

## Quick Links

- [Training LS-Imagine in MineDojo](#training-ls-imagine-in-minedojo)
  - [U-Net Finetuning for Affordance Map Generation](#u-net-finetuning-for-affordance-map-generation)
  - [World Model and Behavior Learning](#world-model-and-behavior-learning)
- [Success Rate Evaluation](#success-rate-evaluation)
- [Citation](#citation)
- [Credits](#credits)

<a name="lsimagine_train"></a>

## Training LS-Imagine in MineDojo
LS-Imagine mainly consists of two stages: [fine-tuning a multimodal U-Net for generating affordance maps](#unet_finetune), [learning world models and behaviors](#agent_learn). 

You can either set up custom tasks in MineDojo ([instructions here](./docs/task_setups.md)) or use the task setups mentioned in our [paper](https://arxiv.org/pdf/2410.03618). LS-Imagine allows to start from any stage of the pipeline, as we provide corresponding checkpoint files for each stage to ensure flexibility.

<a name="unet_finetune"></a>
### U-Net Finetuning for Affordance Map Generation

1. Download the pretrained U-Net weights from [here](https://drive.google.com/file/d/1N2VTC458txxW5UABQDgmRTEYzeYTEjIX/view?usp=sharing) and save them to `./affordance_map/pretrained_unet_checkpoint/swin_unet_checkpoint.pth`.

2. Set up the task ([instructions here](./docs/task_setups.md)) and run the following command to collect data:
    ```bash
    sh ./script/collect.sh your_task_name
    ```

3. Annotate the collected data using a method based on sliding bounding box scanning and simulated exploration to generate the fine-tuning dataset:
    ```bash
    sh ./scripts/affordance.sh your_task_name your_prompt
    ```

4. Fine-tune the pretrained U-Net weights using the annotated dataset to generate task-specific affordance maps:
    ```bash
    sh ./scripts/finetune_unet.sh your_task_name
    ```

5. After training, the fine-tuned multimodal U-Net weights for the specified task will be saved in `./affordance_map/model_out`.

<a name="agent_learn"></a>
### World Model and Behavior Learning

Before starting the learning process for the world model and behavior, ensure you have obtained the multimodal U-Net weights. We provide the pretrained U-Net weights ([link here](https://drive.google.com/file/d/1N2VTC458txxW5UABQDgmRTEYzeYTEjIX/view?usp=sharing)) and the task-specific fine-tuned U-Net weights: 
<div align="center">

| Task Name                  | Weight File                                                                                                                   |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| harvest_log_in_plains      | [swin_unet_checkpoint_log.pth](https://drive.google.com/file/d/1UxLGThaI7_iJ0AR_rNZ4RSQwrSydFN40/view?usp=sharing)             |
| harvest_water_with_bucket  | [swin_unet_checkpoint_water.pth](https://drive.google.com/file/d/1Z-7vDNOiKxFE0iaApjYznALkLu8F4cXD/view?usp=sharing)          |
| harvest_sand               | [swin_unet_checkpoint_sand.pth](https://drive.google.com/file/d/1ZeKVY6Y99Nch_wDXOgl_WX1IEyuIFNrs/view?usp=sharing)          |
| mine_iron_ore              | [swin_unet_checkpoint_iron.pth](https://drive.google.com/file/d/1_sUWXeVEFEYHpQmw0115pMFYJxKmMZyL/view?usp=sharing)          |
| shear_sheep                | [swin_unet_checkpoint_wool.pth](https://drive.google.com/file/d/1cIbkZlxdZtG4hVVErCCbBxoH8MoRLuZF/view?usp=sharing)          |

</div>

You can download these weights using the links provided in the table below and place them at `./affordance_map/finetune_unet/finetune_checkpoints/{task_name}/swin_unet_checkpoint.pth`: 

1. Set up the task and correctly configure the `unet_checkpoint_dir` to ensure the U-Net weights are properly located and loaded ([instructions here](./docs/task_setups.md)).

2. Run the following command to start training the world model and behavior:
    ```bash
    sh ./scripts/train.sh your_task_name
    ```

<a name="evaluation"></a>
## Success Rate Evaluation

After completing the training, the agent's weight file `latest.pt` will be saved in the `./logdir` directory. You can evaluate the performance of LS-Imagine as mentioned in [here](#evaluation_with_checkpoints).
<!--
Additionally, we provide pretrained weights for the tasks mentioned in the paper. You can download them using the links in the table below and rename the downloaded file to `latest.pt`:

<div align="center">

| Task Name                  | Weight File                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------|
| harvest_log_in_plains      | [latest_log.pt](https://drive.google.com/file/d/1_mhz49YPJDMNmPB-WwbzCG6zCTUidFQ3/view?usp=drive_link)                                                                |
| harvest_water_with_bucket  | [latest_water.pt](https://drive.google.com/file/d/1DxtQ-ZckTVw1tFySspKRaxoaShDi_b8A/view?usp=drive_link)                                                              |
| harvest_sand               | [latest_sand.pt](https://drive.google.com/file/d/1xa6JwV7rh-IfGoFjWDoneWpaTwPxLWb_/view?usp=drive_link)                                                               |
| mine_iron_ore              | [latest_iron.pt](https://drive.google.com/file/d/1FOIRGQJvgeQptK8-4cVVGv_jeNIy8kw7/view?usp=drive_link)                                                               |
| shear_sheep                | [latest_wool.pt](https://drive.google.com/file/d/1sx7IVOZ1JYs0BJHD3TWZcPb-f-x5xfA3/view?usp=drive_link)                                                               |

</div>


1. Set up the task for evaluation ([instructions here](./docs/task_setups.md)).
2. Retrieve your **Weights & Biases (wandb)** API key and set it in the `./config.yaml` file under the field `wandb_key: {your_wandb_api_key}`.
3. Run the following command to test the success rate:
    ```bash
    MINEDOJO_HEADLESS=1 python test.py \
        --configs minedojo \
        --task minedojo_test_harvest_log_in_plains \
        --logdir ./logdir \
        --agent_checkpoint_dir {path_to_latest.pt} \
        --eval_episode_num 100
    ```
    -->

## Citation 
If you find this repo useful, please cite our paper:
```bib
@inproceedings{li2025open,
    title={Open-World Reinforcement Learning over Long Short-Term Imagination}, 
    author={Jiajian Li and Qi Wang and Yunbo Wang and Xin Jin and Yang Li and Wenjun Zeng and Xiaokang Yang},
    booktitle={ICLR},
    year={2025}
}
```


## Credits [🔝](#quick-links)
The codes refer to the implemention of [dreamerv3-torch](https://github.com/NM512/dreamerv3-torch) and [Swin-Unet](https://github.com/HuCaoFighting/Swin-Unet). Thanks for the authors！

