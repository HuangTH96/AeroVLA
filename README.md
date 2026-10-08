# 1. Setup

1. setup conda env for CUDA_VERSION: 13.0
  ```bash
  git clone https://github.com/XuPeng23/AeroVLA.git
  cd AeroVLA

  conda create -n aero_vla python=3.10 -y
  conda activate aero_vla

  pip install -r requirements.txt

  # 手动下载 flash-attn 2.5.8
  wget https://github.com/Dao-AILab/flash-attention/releases/download/v2.5.8/flash_attn-2.5.8+cu122torch2.1cxx11abiFALSE-cp310-cp310-linux_x86_64.whl
  pip install flash_attn-2.5.8+cu122torch2.1cxx11abiFALSE-cp310-cp310-linux_x86_64.whl --no-deps

  # 手动下载 msgpack-rpg-python
  git clone https://github.com/tbelhalfaoui/msgpack-rpc-python.git
  cd msgpack-rpc-python
  git checkout fix-msgpack-dep
  python setup.py install
  ```

2. setup Dataset and envs. 因为在配置[TravelUAV](https://github.com/HuangTH96/TravelUAV/tree/main)时，已经下载好数据集和环境了，所以只要满足项目结构（查看 [Project Structure](#project-structure)），即可通过**软连接**的方式连接到相关文件夹，不用重复下载
  ```bash
  cd <path-to-AeroVLA>
  mkdir dataset_raw/ envs/

  ln -s /data/huangth/TravelUAV_dataset/extracted/* ./dataset_raw
  ln -s /data/huangth/TravelUAV_env/extracted/* ./envs
  ```

3. Download checkpoints for Models
  ```bash
  mkdir -p openvla-7b/ checkpoints/aerial_vla/

  ```


## Project Structure
```
AeroVLA/
├── airsim_plugin/
├── checkpoints/
├── data/                 
│   ├── meta/             
│   ├── uav_dataset/
│   └── aerovla_train_dataset.json   
├── dataset_raw/
│   ├── BattlefieldKitDesert/     
│   ├── BrushifyCountryRoads/   
│   └── ...               
├── envs/
│   ├── carla_town_envs/     
│   ├── closeloop_envs/
│   ├── extra_envs/
│   └── ...               
├── eval_results/         
├── openvla-7b/
├── scripts/
│   ├── eval_aerovla.sh 
│   └── metric.sh         
├── src/
│   ├── model_wrapper/
│   ├── vlnce_src/
│   ├── aerovla_dataset.py
│   └── train_aerovla.py   
└── utils/                
```
