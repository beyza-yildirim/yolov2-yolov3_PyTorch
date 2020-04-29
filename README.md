# the whole project
In this project, you can enjoy yolo-v2, yolo-v3, tiny-yolo-v2 and tiny-yolo-v3. What I have to say is that I don't try to 100% reproduce official YOLO, because it is really difficult and I have not much computation resource. 

Recently, I made some improvement, and my yolo project is very close to official yolo models.

I will upload the new model again. Just hold on~

However, I have a qeustion: Is the mAP metric really good? Does it really suit object detection?

I find higher mAP doesn't mean better visualization...so weird.

# pytorch-yolo-v3
Good news !!!

In this update, I add yolo-v3 model. For more details, you could see code files including ```models/yolo_v3.py``` and ```tools.py```.

Recently, I made some improvement, and my yolo-v3 is being closer and closer to official yolo-v3.

The new model is being trained, and I will upload it in time. Just hold on~

In addition, you can replace darknet-53 with darknet-19 as the backbone of yolo-v3.

# pytorch-yolo-v2
I really enjoy yolo. It is so amazing! So I try to reproduce it. And I think I achieve this goal:

<table><tbody>
<tr><th align="left" bgcolor=#f8f8f8> </th>     <td bgcolor=white> size </td><td bgcolor=white> Original (darknet) </td><td bgcolor=white> Ours (pytorch) </td></tr>
<tr><th align="left" bgcolor=#f8f8f8> VOC07 test</th><td bgcolor=white> 416 </td><td bgcolor=white> 76.8 </td><td bgcolor=white> 77.1 </td></tr>
<tr><th align="left" bgcolor=#f8f8f8> VOC07 test</th><td bgcolor=white> 544 </td><td bgcolor=white> 78.6 </td><td bgcolor=white> 78.1 </td></tr>
</table></tbody>


## Tricks
Tricks in official paper:
- [x] batch norm
- [x] hi-res classifier
- [x] convolutional
- [x] anchor boxes
- [x] new network
- [x] dimension priors
- [x] location prediction
- [x] passthrough
- [x] multi-scale
- [x] hi-red detector

In TITAN Xp, my yolo-v2 runs at 100+ FPS, so it's very fast. I have no any TITAN X GPU, and I can't run my model in a X GPU. Sorry, guys~

Before I tell you how to use this project, I must say one important thing about difference between origin yolo-v2 and mine:

- For data augmentation, I copy the augmentation codes from the https://github.com/amdegroot/ssd.pytorch which is a superb project reproducing the SSD. If anyone is interested in SSD, just clone it to learn !(Don't forget to star it !)

So I don't write data augmentation by myself. I'm a little lazy~~

My loss function and groundtruth creator both in the ```tools.py```, and you can try to change any parameters to improve the model.

Next, I plan to train my yolo-v2 on COCO.

## Installation
- Pytorch-gpu 1.1.0/1.2.0/1.3.0
- Tensorboard 1.14.
- opencv-python, python3.6/3.7

## Dataset
As for now, I only train and test on PASCAL VOC2007 and 2012. 

### VOC Dataset
I copy the download files from the following excellent project:
https://github.com/amdegroot/ssd.pytorch

I have uploaded the VOC2007 and VOC2012 to BaiDuYunDisk, so for researchers in China, you can download them from BaiDuYunDisk:

Link：https://pan.baidu.com/s/1tYPGCYGyC0wjpC97H-zzMQ 

Password：4la9

You will get a ```VOCdevkit.zip```, then what you need to do is just to unzip it and put it into ```data/```. After that, the whole path to VOC dataset is ```data/VOCdevkit/VOC2007``` and ```data/VOCdevkit/VOC2012```.

#### Download VOC2007 trainval & test

```Shell
# specify a directory for dataset to be downloaded into, else default is ~/data/
sh data/scripts/VOC2007.sh # <directory>
```

#### Download VOC2012 trainval
```Shell
# specify a directory for dataset to be downloaded into, else default is ~/data/
sh data/scripts/VOC2012.sh # <directory>
```

### MSCOCO Dataset
I copy the download files from the following excellent project:
https://github.com/DeNA/PyTorch_YOLOv3

#### Download MSCOCO 2017 dataset
Just run data/scripts/COCO2017.sh


## Train
To run:
```Shell
python train_voc.py -v yolo_v2 -hr -ms --cuda
```

You can run ```python train_voc.py -h``` to check all optional argument.

By default, I set num_workers in pytorch dataloader as 0 to guarantee my multi-scale trick. But the trick can't work when I add more wokers. I know little about multithreading. So sad...

## Test
To run:
```Shell
python test_voc.py --trained_model [ Please input the path to model dir. ]
```

## Evaluation
To run:
```Shell
python eval_voc.py --train_model [ Please input the path to model dir. ]
```

Finally, I have tried to train my yolo-v2 on MSCOCO-2017 datatset, but I didn't get a good result. My yolo-v2 got 31.5 AP50 on MSCOCO-valid dataset and its visualization results are a little poor. I haven't address this problem , but what I know is that MSCOCO is really a challenging dataset !
