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

sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo apt-get update
sudo apt-get install python3-certbot-nginx -y

sudo certbot --nginx

sudo service nginx restart