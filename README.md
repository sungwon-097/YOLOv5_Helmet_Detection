# ๐ Open Source design baSic _ Project
## โ๏ธ Detects wearing a helmet

|Team 11|Weeks|Distributing roles|
|-|-|-|
|-|Week1|๊ฐ๋ฐํ๊ฒฝ์ ์ธํ, `Dataset` ์ค๋น ๋ฐ ๋ผ๋ฒจ๋ง ์์|
|-|WeeK2|๋ผ๋ฒจ๋ง๋ ์ด๋ฏธ์ง๋ฅผ `Yolov5s`๋ฅผ ์ด์ฉํด ํ์ต์ํด|
|-|WeeK3|์ค์ ๊ฐ์ ๋ณ๊ฒฝํ๋ฉฐ ์ํ๋ ๊ฒฐ๊ณผ๊ฐ ๋์ฌ ๋๊น์ง ํ์คํธ๋ฅผ ์งํ|

## Needs

- >pyTorch ๊ธฐ๋ฐ Yolov5
- >Cuda, Cudnn ์ ๊ฒฝ๋ง

* * *
## Summary :
```
์ด์ ์์ ์์ ๋ชจ ์ฐฉ์ฉ ์ ๋ฌด๋ฅผ ํ์ธํ์ฌ ๋ฏธ์ฐฉ์ฉ์ ๊ฒฝ๊ณ ์์ ์ถ๋ ฅํ๋ค.

Yolov5 ํ๋ ์์ํฌ ์คํ์์ค๋ฅผ ์ฌ์ฉํ์ฌ ์์ ๋ชจ ์ฐฉ์ฉ๋ชจ์ต์ ํ์ต์ํด.
์ธ์์ ์คํจํ  ๊ฒฝ์ฐ ๊ฒฝ๊ณ ์์ ๋ด๋ณด๋ธ๋ค

๋จธ๋ฆฌ๋ฅผ ๋ณดํธ ํ  ์ ์๋ ์์  ์ฅ๋น๋ผ๋ฉด(๋ชจ์๋ ๋ฐฉํ์ฉํ์ ์ ์ธ) ๋ชจ๋ ์ธ์์ด ๋  ์ 
์๋๋ก ์ ๋ขฐ๋๊ฐ ๋์ dataset์ ์ค๋นํด์ผํ๋ค.

Detection์ด ์ฑ๊ณต์ ์ผ๋ก ์ด๋ค์ง๋ค๋ฉด ์ค์์ด๋ ์ฌ๋ง์ฌ๊ณ ๋ฅผ ์ค์ผ ์ ์๋ ๋ฐฉ์์ด ๋  ๊ฒ์ด๋ค.
๋ํ, ์ด์ฉ์๋ค์ ์์  ์ฅ๋น ์ฐฉ์ฉ์ ๋ํ ์ธ์ ๊ฐ์ ์๋ ๊ธฐ์ฌํ  ๊ฒ์ผ๋ก ๊ธฐ๋๊ฐ ๋๋ค
```

## Thanks for


- Yolov5 Framework : [Yolov5](https://github.com/ultralytics/yolov5.git, "Yolov5 link")

- LabelImg : [labelImg](https://github.com/tzutalin/labelImg.git, "labelImg link")

- Roboflow : [labelImg](https://roboflow.com/, "Roboflow link")

## Graph

![img](graph.PNG)

# How to Use?

### Labeling

- https://github.com/tzutalin/labelImg.git

```

$ git clonehttps://github.com/tzutalin/labelImg.git
$ cd labelImg
$ python labelimg

# class์ names์ ๋ง๊ฒ labeling ์งํ

$ git clone https://github.com/ultralytics/yolov5  # clone repo
$ cd yolov5
$ git reset --hard 886f1c03d839575afecb059accf74296fad395b6

# clone YOLOv5 repository

$ cd /content/yolov5
$ cat ../data.yaml

    train: ../train/images
    val: ../valid/images

    nc: 2
    names: ['With Helmet', 'Without Helmet']

# yamlํ์ผ ์์ฑ ํ ํ์ธ

$ python train.py --img 416 --batch 16 --epochs 100 --data '../data.yaml' --cfg ./models/custom_yolov5s.yaml --weights '' --name yolov5s_results  --cache

                    from n    params  module                                  arguments                     
    0                -1  1      3520  models.common.Focus                     [3, 32, 3]                    
    1                -1  1     18560  models.common.Conv                      [32, 64, 3, 2]                
    2                -1  1     19904  models.common.BottleneckCSP             [64, 64, 1]                   
    3                -1  1     73984  models.common.Conv                      [64, 128, 3, 2]               
    4                -1  1    161152  models.common.BottleneckCSP             [128, 128, 3]                 
    5                -1  1    295424  models.common.Conv                      [128, 256, 3, 2]              
    6                -1  1    641792  models.common.BottleneckCSP             [256, 256, 3]                 
    7                -1  1   1180672  models.common.Conv                      [256, 512, 3, 2]              
    8                -1  1    656896  models.common.SPP                       [512, 512, [5, 9, 13]]        
    9                -1  1   1248768  models.common.BottleneckCSP             [512, 512, 1, False]          
    10                -1  1    131584  models.common.Conv                      [512, 256, 1, 1]              
    11                -1  1         0  torch.nn.modules.upsampling.Upsample    [None, 2, 'nearest']          
    12           [-1, 6]  1         0  models.common.Concat                    [1]                           
    13                -1  1    378624  models.common.BottleneckCSP             [512, 256, 1, False]          
    14                -1  1     33024  models.common.Conv                      [256, 128, 1, 1]

# training

$ python detect.py --weights runs/train/yolov5s_results/weights/best.pt --img 416 --conf 0.3 --source ../test/images

    /content/yolov5
    Namespace(agnostic_nms=False, augment=False, classes=None, conf_thres=0.3, device='', exist_ok=False, img_size=416, iou_thres=0.45, name='exp', project='runs/detect', save_conf=False, save_txt=False, source='../test/images', update=False, view_img=False, weights=['runs/train/yolov5s_results/weights/best.pt'])

# test image Detection
```