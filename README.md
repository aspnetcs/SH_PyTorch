# Spectral Hashing
http://papers.nips.cc/paper/3383-spectral-hashing.pdf

http://papers.nips.cc/paper/3383-spectral-hashing

http://www.cs.huji.ac.il/~yweiss/SpectralHashing/

## Reference
Weiss Y , Torralba A , Fergus R . Spectral Hashing[C]// Advances in Neural Information Processing Systems 21, Proceedings of the Twenty-Second Annual Conference on Neural Information Processing Systems, Vancouver, British Columbia, Canada, December 8-11, 2008. Curran Associates Inc. 2008.

## REQUIREMENTS
`pip install -r requirements.txt`

1. pytorch >= 1.0
2. loguru

## DATASETS
1. [cifar10-gist.mat](https://pan.baidu.com/s/1qE9KiAOTNs5ORn_WoDDwUg) password: umb6
2. [cifar-10_alexnet.t](https://pan.baidu.com/s/1ciJIYGCfS3m0marQvatNjQ) password: f1b7
3. [nus-wide-tc21_alexnet.t](https://pan.baidu.com/s/1YglFwoxB-3j7xTEyAc8ykw) password: vfeu
4. [imagenet-tc100_alexnet.t](https://pan.baidu.com/s/1ayv4wdtCOzEDsJy01SjRew) password: 6w5i

## USAGE
```
usage: run.py [-h] [--dataset DATASET] [--root ROOT]
              [--code-length CODE_LENGTH] [--topk TOPK] [--gpu GPU]
              [--seed SEED]

SH_PyTorch

optional arguments:
  -h, --help            show this help message and exit
  --dataset DATASET     Dataset name.
  --root ROOT           Path of dataset
  --code-length CODE_LENGTH
                        Binary hash code length.(default:
                        8,16,24,32,48,64,96,128)
  --topk TOPK           Calculate map of top k.(default: ALL)
  --gpu GPU             Using gpu.(default: False)
  --seed SEED           Random seed.(default: 3367)
```
## Example
Put these data sets (cifar10-gist.mat,cifar-10_alexnet.t,nus-wide-tc21_alexnet.t,imagenet-tc100_alexnet.t) in the data directory,and then run the following command.

**python run.py --dataset cifar-10 --root .\data\cifar-10_alexnet.t**

2020-06-02 03:04:53.522 | INFO     | __main__:run:39 - [code_length:8][map:0.1819]

2020-06-02 03:05:10.976 | INFO     | __main__:run:39 - [code_length:16][map:0.1866]

2020-06-02 03:05:33.668 | INFO     | __main__:run:39 - [code_length:24][map:0.1920]

2020-06-02 03:06:02.806 | INFO     | __main__:run:39 - [code_length:32][map:0.1901]

2020-06-02 03:06:47.982 | INFO     | __main__:run:39 - [code_length:48][map:0.2050]

2020-06-02 03:07:56.644 | INFO     | __main__:run:39 - [code_length:64][map:0.2017]

2020-06-02 03:09:48.745 | INFO     | __main__:run:39 - [code_length:96][map:0.1984]

2020-06-02 03:12:42.339 | INFO     | __main__:run:39 - [code_length:128][map:0.1965]

**python run.py --dataset cifar10-gist --root .\data\cifar_10_gist.mat**

2020-06-10 07:31:05.195 | INFO     | __main__:run:39 - [code_length:8][map:0.1247]

2020-06-10 07:31:07.091 | INFO     | __main__:run:39 - [code_length:16][map:0.1302]

2020-06-10 07:31:09.432 | INFO     | __main__:run:39 - [code_length:24][map:0.1291]

2020-06-10 07:31:12.158 | INFO     | __main__:run:39 - [code_length:32][map:0.1283]

2020-06-10 07:31:16.171 | INFO     | __main__:run:39 - [code_length:48][map:0.1310]

2020-06-10 07:31:22.579 | INFO     | __main__:run:39 - [code_length:64][map:0.1286]

2020-06-10 07:31:33.724 | INFO     | __main__:run:39 - [code_length:96][map:0.1288]

2020-06-10 07:31:51.210 | INFO     | __main__:run:39 - [code_length:128][map:0.1274]



**python run.py --dataset imagenet-tc100 --root .\data\imagenet-tc100_alexnet.t**


2020-06-09 23:35:15.200 | INFO     | __main__:run:39 - [code_length:8][map:0.0523]

2020-06-09 23:39:26.470 | INFO     | __main__:run:39 - [code_length:16][map:0.0888]

2020-06-09 23:44:32.683 | INFO     | __main__:run:39 - [code_length:24][map:0.1095]

2020-06-09 23:50:49.251 | INFO     | __main__:run:39 - [code_length:32][map:0.1315]

2020-06-09 23:59:08.057 | INFO     | __main__:run:39 - [code_length:48][map:0.1545]

2020-06-10 00:09:40.343 | INFO     | __main__:run:39 - [code_length:64][map:0.1654]

2020-06-10 00:24:35.635 | INFO     | __main__:run:39 - [code_length:96][map:0.1805]

2020-06-10 00:43:28.329 | INFO     | __main__:run:39 - [code_length:128][map:0.1844]


**python run.py --dataset nus-wide-tc21 --root .\data\nus-wide-tc21_alexnet.t**



2020-06-01 14:31:07.025 | INFO     | __main__:run:39 - [code_length:8][map:0.4062]

2020-06-01 14:33:20.802 | INFO     | __main__:run:39 - [code_length:16][map:0.4112]

2020-06-01 14:36:15.478 | INFO     | __main__:run:39 - [code_length:24][map:0.4185]

2020-06-01 14:39:47.755 | INFO     | __main__:run:39 - [code_length:32][map:0.4448]

2020-06-01 14:44:36.249 | INFO     | __main__:run:39 - [code_length:48][map:0.4332]

2020-06-01 14:50:49.982 | INFO     | __main__:run:39 - [code_length:64][map:0.4315]

2020-06-01 15:01:05.612 | INFO     | __main__:run:39 - [code_length:96][map:0.4253]

2020-06-01 15:14:49.145 | INFO     | __main__:run:39 - [code_length:128][map:0.4236]


## EXPERIMENTS
cifar10-gist dataset. Gist features, 1000 query images, 5000 training images, MAP@ALL.

cifar-10-alexnet dataset. Alexnet features, 1000 query images, 5000 training images, MAP@ALL.

nus-wide-tc21-alexnet dataset. Alexnet features, top 21 classes, 2100 query images, 10500 training images, MAP@5000.

imagenet-tc100-alexnet dataset. Alexnet features, top 100 classes, 5000 query images, 10000 training images, MAP@1000.

   Bits     | 8 | 16 | 24 | 32 | 48 | 64 | 96 | 128 
   ---        |   ---  |   ---   |   ---   |   ---   |   ---   |   ---   |   ---   |   ---   
  cifar10-gist@ALL  | 0.1246 | 0.1303 | 0.1290 | 0.1283 | 0.1310 | 0.1286 | 0.1288  | 0.1274
  cifar10-alexnet@ALL | 0.1890 | 0.1863 | 0.1912 | 0.1892 | 0.2044 | 0.2013 | 0.1978 | 0.1960
  nus-wide-tc21-alexnet@5000 | 0.5503 | 0.5615 | 0.5886 | 0.6402 | 0.6309 | 0.6350 | 0.6344 | 0.6411
  imagenet-tc100-alexnet@1000 | 0.0961 | 0.2013 | 0.2421 | 0.2806 | 0.3235 | 0.3445 | 0.3747 | 0.3908

