# 3d gaussian slatting slam

ref https://github.com/WangFeng18/3d-gaussian-splatting

ref https://github.com/luigifreda/pyslam

ref https://github.com/LiheYoung/Depth-Anything

test vo
```bash
docker build  -t 3dgs_slam:0.1.0 .
docker run -it --rm -e "DISPLAY=$DISPLAY" -v /tmp/.X11-unix:/tmp/.X11-unix -v ./:/app --privileged --gpus all 3dgs_slam:0.1.0 bash
python3 ./src/main_vo.py
```
test cuda
```bash
docker build  -t 3dgs_slam:0.1.0 .
docker run -it --rm -e  "DISPLAY=$DISPLAY" -v /tmp/.X11-unix:/tmp/.X11-unix -v ./:/app --privileged --gpus all 3dgs_slam:0.1.0 bash
cd ./src/gaussian
python3 setup.py install
```

test depth estimator
1. create dataset/data dir and dataset/result dir
2. put ur demo images in dataset/data
3. download the pretrained model from https://huggingface.co/spaces/LiheYoung/Depth-Anything/blob/main/checkpoints/depth_anything_vits14.pth
4. move it into src/depth_estimator/depth_anything/checkpoints/
5. run on docker
```bash
docker build  -t 3dgs_slam:0.1.0 .
docker run -it --rm -e  "DISPLAY=$DISPLAY" -v /tmp/.X11-unix:/tmp/.X11-unix -v ./:/app --privileged --gpus all 3dgs_slam:0.1.0 bash
python3 src/depth_estimator/run.py
```

ug note
to build orbslam3
apt-get install libboost-all-dev
sudo apt-get install libssl-dev
cd ORB_SLAM3
rm -rf build
./build.sh

./ORB_SLAM3/Examples/Monocular/mono_euroc \
ORB_SLAM3/Vocabulary/ORBvoc.txt \
ORB_SLAM3/Examples/Monocular/EuRoC.yaml \
dataset/EuRoc/MH01/ \
ORB_SLAM3/Examples/Monocular/EuRoC_TimeStamps/MH01.txt

