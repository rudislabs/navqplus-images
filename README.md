# NavQPlus Ubuntu 22.04 ROS 2 Humble images on 6.x.x kernels
See releases

## Flash image with `uuu` to emmc
### Boot switches
Make sure boot switches are in flash mode:
![image](https://user-images.githubusercontent.com/10233412/235987123-838d5295-149f-4258-b98f-96aa24345b35.png)
| Mode  | Switch 1 | Switch 2 |
| ----- | -------- | -------- |
|  SD   |    ON    |    ON    |
| eMMC  |    OFF   |    ON    |
| Flash |    ON    |    OFF   |
### Uncompress image for flashing faster
```bash
unzstd navqplus-image-22.04-humble-<date>.wic.zst
```
### Flash image with `uuu` to emmc
```bash
sudo ./uuu -b emmc_all navqplus-image-22.04-humble-<date>.bin-flash_evk navqplus-image-22.04-humble-<date>.wic
```



## Build steps for current image release:
### Setup Docker
#### Clone Docker repository
```bash
mkdir -p /home/$USER/git
cd /home/$USER/git
git clone git@github.com:rudislabs/docker-imx-builder.git
```
#### Install Docker (with docker compose)
```bash
cd /home/$USER/git/docker-imx-builder/navqplusbuilder/install
./docker.sh
```
#### Build Docker
```bash
cd /home/$USER/git/docker-imx-builder/navqplusbuilder
docker compose build
```

### Build NavQPlus Humble image in Docker
#### Run Docker
```bash
cd /home/$USER/git/docker-imx-builder/navqplusbuilder
docker compose run navqplusbuilder
```
#### Run Humble build script in navqplusbuilder Docker
```bash
wget https://raw.githubusercontent.com/rudislabs/meta-navqplus-apt-ros/imx-6.1.22-humble/scripts/build.sh
chmod a+x build.sh
./build.sh
```
