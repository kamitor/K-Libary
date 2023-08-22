apt install pip -y
pip install 'torch>=2.0'

pip install -U audiocraft  
pip install -U git+https://git@github.com/facebookresearch/audiocraft#egg=audiocraft  
pip install -e . 

sudo apt-get install ffmpeg
git clone https://github.com/facebookresearch/audiocraft.git
python setup.py