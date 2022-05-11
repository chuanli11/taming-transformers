# Setup

```
# From your home directory
mkdir lambda
cd lambda

git clone https://github.com/chuanli11/taming-transformers.git
cd taming-transformers
git checkout lambda/hl

# Download https://drive.google.com/file/d/1xf89g0mc78J3d8Bx5YhbK4tNRNlOoYaO/edit
# unzip and put the folder open_images_distilled_e_60 into ~/lambda/taming-transformers/logs

mkdir results


# Launch Docker container
docker_image=vault.habana.ai/gaudi-docker/1.4.0/ubuntu20.04/habanalabs/pytorch-installer-1.10.2:1.4.0-442
sudo docker run --rm -it --runtime=habana --shm-size=8gb -e HABANA_VISIBLE_DEVICES=all --volume ~/lambda:/lambda $docker_image

cd lambda/taming-transformers

pip uninstall Pillow && \
pip install Pillow==9.0.1 && \
pip install pytorch-lightning && \
pip install -r requirements.txt && \
pip install -e .


# Run job
python scripts/make_scene_samples.py --outdir=results -r logs/open_images_distilled_e_60/ --resolution=512,512
```
