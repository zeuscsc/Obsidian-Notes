~~~shell
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
conda create --name art python=3.10.6
conda activate art
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu116
git clone https://github.com/zeuscsc/anime-manga-creation-helper.git
pip install -r requirements_versions.txt
sudo apt update -y
sudo apt upgrade -y
sudo apt install nginx -y
sudo nano /etc/nginx/sites-available/default
location / {
    proxy_pass http://localhost:7860;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}

sudo nano /etc/nginx/nginx.conf
   proxy_read_timeout 360000;
   proxy_connect_timeout 360000;
   proxy_send_timeout 360000;
   client_max_body_size 1024M;

sudo nginx -t

sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo apt-get update
sudo apt-get install python3-certbot-nginx -y

sudo certbot --nginx

sudo service nginx restart

ssh mlc -o TCPKeepAlive=yes -o ServerAliveCountMax=20 -o ServerAliveInterval=15

forever start -c "bash ./art.sh" .
switch_cuda 11.7
nvcc --version


sudo apt install build-essential
conda create --name tts python=3.7
conda activate tts
conda install -y -c conda-forge sox libsndfile swig bzip2 libflac bc
pip install pytest-runner -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install paddlepaddle -i https://mirror.baidu.com/pypi/simple
pip install paddlespeech -i https://pypi.tuna.tsinghua.edu.cn/simple
python3 -m pip install paddlepaddle-gpu==2.4.1 -i https://mirror.baidu.com/pypi/simple

wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
chmod +x cuda_10.2.89_440.33.01_linux.run
sudo ./cuda_10.2.89_440.33.01_linux.run --toolkit --silent --override --no-opengl-libs
nano ~/.bashrc
switch_cuda() {
    if [ "$1" = "10.2" ]; then
        export PATH=$(echo $PATH | awk -v RS=: -v ORS=: '!/cuda/ {print}' | sed 's/:$//'):/usr/local/cuda-10.2/bin
        export LD_LIBRARY_PATH=$(echo $LD_LIBRARY_PATH | awk -v RS=: -v ORS=: '!/cuda/ {print}' | sed 's/:$//'):/usr/local/cuda-10.2/lib64
    elif [ "$1" = "11.7" ]; then
        export PATH=$(echo $PATH | awk -v RS=: -v ORS=: '!/cuda/ {print}' | sed 's/:$//'):/usr/local/cuda-11.7/bin
        export LD_LIBRARY_PATH=$(echo $LD_LIBRARY_PATH | awk -v RS=: -v ORS=: '!/cuda/ {print}' | sed 's/:$//'):/usr/local/cuda-11.7/lib64
    else
        echo "Unsupported CUDA version. Please use '10.2' or '11.7'"
    fi
}
switch_cuda 10.2
nvcc --version

cd ~/PaddleSpeech/examples/canton/tts3

source path.sh
FLAGS_allocator_strategy=naive_best_fit \
FLAGS_fraction_of_gpu_memory_to_use=0.01 \
python ${BIN_DIR}/../synthesize_e2e.py \
  --am=fastspeech2_aishell3 \
  --am_config=fastspeech2_canton_ckpt_1.4.0/default.yaml \
  --am_ckpt=fastspeech2_canton_ckpt_1.4.0/snapshot_iter_140000.pdz \
  --am_stat=fastspeech2_canton_ckpt_1.4.0/speech_stats.npy \
  --voc=pwgan_aishell3 \
  --voc_config=pwg_aishell3_ckpt_0.5/default.yaml \
  --voc_ckpt=pwg_aishell3_ckpt_0.5/snapshot_iter_1000000.pdz \
  --voc_stat=pwg_aishell3_ckpt_0.5/feats_stats.npy \
  --lang=canton \
  --text=${BIN_DIR}/../sentences_canton.txt \
  --output_dir=exp/default/test_e2e \
  --phones_dict=fastspeech2_canton_ckpt_1.4.0/phone_id_map.txt \
  --speaker_dict=fastspeech2_canton_ckpt_1.4.0/speaker_id_map.txt \
  --spk_id=10 \
  --inference_dir=exp/default/inference




