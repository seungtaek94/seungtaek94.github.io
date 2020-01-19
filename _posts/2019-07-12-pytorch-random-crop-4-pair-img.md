---
layout: post
title: '[PyTorch] Pair 이미지를 위한 RandomCrop'
subtitle: ''
categories: programing
tags: pytorch
comments: true
---
## 문제
 Pair 이미지를 가지고 GAN을 학습하기 위해서, Torchvision의 transform을 이용했지만 Pair 이미지에 적용할때 각 이미지에 각각 Rnadom Crop이 적용되 Pair 이미지의 Random Crop된 부분이 다른 문제가 있었다.

## 해결 과정
Paired 이미지를 Dataloader에 주기 위한 CustomDataset의 구조는 아래와 같다.

```python
class CustomDataset(Dataset):
    def __init__(self, image1_paths, image2_paths, transform=None):
        self.image1_paths = [f for f in listdir(data_path_A) if isfile(join(data_path_A, f))]
        self.image2_paths = [f for f in listdir(data_path_B) if isfile(join(data_path_B, f))]
        self.transform = transform
        
    def __getitem__(self, index):
        img1 = Image.open(data_path_A+self.image1_paths[index])
        img2 = Image.open(data_path_B+self.image2_paths[index])
        
        if self.transform:
            #transforms.Compos
            img1 = self.transform(img1)
            img2 = self.transform(img2)
            
        return img1, img2
    
    def __len__(self):
        return len(self.image1_paths)
```

```python
trans = transforms.Compose([
    transforms.RandomCrop(256)
    transforms.ToTensor(),    
    transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))
])

dataset = CustomDataset(data_path_A, data_path_B, transform=trans)
```

 나는 아무생각 없이 잘 동작할 거라 생각했지만, Random을 망각했다. Random 이기에 당연히 img1, img2의 크롭된 위치가 달랐다. 이를 해결하기 위해 Compose에 함께 묶여 있는 RandomCrop을 지우고, CustomDataset 안의 transform 하는 부분에 아래의 코드를 추가하 였다.

```python
#RandomCrop For Pair
i, j, h, w = transforms.RandomCrop.get_params(img1, output_size=(256, 256))
img1 = TF.crop(img1, i, j, h, w)
img2 = TF.crop(img2, i, j, h, w)
```

  RandomCrop 클래스의 get_params 함수를 이용해 Random으로 생성된 파라미터 i, j, h, w(i, j는 크롭할 위치의 좌상단) 받아 ttorchvision.transforms.functional(위의 코드에서 TF)의 crop 함수 를 이용해 Crop 하였다.

 위와 같은 방법을 이용하면, Mask를 이용한 Segmentation task, Pair 이미지를 이용한 GAN 모델 학습등에서 RandomCrop을 이용할 수 있을 것이다.