# MNIST Experiment - Targetting 99.4 Test Accuracy with below constraints
    1. # parameters should be less than 8000
    2. # Test Accuracy >= 99.4 in 15 Epochs




<br>

Experiment Table
----------------

<table>
  <thead>
    <tr>
      <th align="center" width="20%"=>Experiments</th>
      <th align="center" width="27%">Model Features</th>
      <th align="center" width="53%;">Analysis</th>
    </tr>
	</thead>
	<tbody>
		<tr>
		    <td><a href="./ERA_4_S6_Exp1.ipynb" target="_blank" rel="noopener noreferrer">1: 1st version </a></td>
			<td>
				<ul>
					<li> Total Parameters : 10.9k </li>
					<li> Training Acc : 99.81% </li>
					<li> Test Acc : 99.22% </li>
				</ul>
			</td>
			<td>
				<ul>
					<li>Achieve 99% Train and Test Accuracy with less than 11000 parameters ( Best Test Accuract 99.22 in 15th Epoch)</li>
					<li>Model started overfitting after 8th epoch</li>
					<li>No Image Augmentation applied, used 7*7 Kernel before last conv block, No AVG Pooling layer</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><a href="./ERA_4_S6_Exp4.ipynb">2: Adding Global Avg Pooling</a></td>
			<td>
				<ul>
					<li> Total Parameters : 7.45k </li>
					<li> Training Acc : 98.94% </li>
					<li> Test Acc : 98.99% </li>
				</ul>
			</td>
			<td>
				<ul>
                    <li>Increase model capacity by adding more channels in initial layer to detect meaningful pattern </li>
					<li>Tried many architecture and come up with this architecture which has enough capacity with in constraints</li>
					<li> Compensated increased capacity in initial layer by reducing parameter in last layer, which was contributed by 7*7 Kernel.</li>
					<li>Used Global Avg Pooling in place of 7*7 Conv layer which will give summary of all featured available in image</li>
                    <li> Gap between Train and test accuracy is very low and gap is reducing on each epoch, currently this is underfitted, if we had train mode we would have inreased accuracy</li>
                    <li>decreasing performance is  because of reduce parameter, but over this is powerful model, and has potential to improve if trained more</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><a href="./exp6.ipynb">3: Best Model with Data Agumentation and Learning Rate Tuning</a></td>
			<td>
				<ul>
					<li> Total Parameters : 7.49k </li>
					<li> Training Acc : 99.17% </li>
					<li> Test Acc : 99.43% </li>
				</ul>
			</td>
			<td>
				<ul>
                    <li> We can start seeing pattern in MNIST in RF 5*5 so added maxpool after 5*5 RF.</li>
					<li>applied Augmentation - e.g Rotation - 5%</li>
					<li>Added more parameter in middle layers to learn combine pattern, increased model capacity gradually from less parameters at initial layer to gradually more parameters in later layers</li>
					<li>After so many experiments found out best Augmentation paramters and learning rate (0.015)</li>
					<li> BINGO ! 😎 Achieved Target 99.4 Test Accuracy twice (9th and 12th epoch) </li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>


# Receptive Field Table 



Below are the tables of receptive fields (RF) for each layer of the provided models. The receptive field size at each layer is calculated based on the kernel size, stride, and padding.

### **Net1 Receptive Field Table**
| Layer        | Output Size | Kernel Size | Stride | Padding | RF  |
|--------------|-------------|-------------|--------|---------|-----|
| Input        | 28×28       | —           | —      | —       | 1   |
| Conv2d-1     | 26×26       | 3×3         | 1      | 0       | 3   |
| Conv2d-4     | 24×24       | 3×3         | 1      | 0       | 5   |
| Conv2d-7     | 22×22       | 3×3         | 1      | 0       | 7   |
| MaxPool2d-10 | 11×11       | 2×2         | 2      | 0       | 8   |
| Conv2d-11    | 11×11       | 1×1         | 1      | 0       | 8   |
| Conv2d-14    | 9×9         | 3×3         | 1      | 0       | 12  |
| Conv2d-17    | 7×7         | 3×3         | 1      | 0       | 16  |
| Conv2d-20    | 7×7         | 1×1         | 1      | 0       | 16  |
| Conv2d-23    | 1×1         | 7×7         | 1      | 0       | 28  |

---

### **Net2 Receptive Field Table**
| Layer        | Output Size | Kernel Size | Stride | Padding | RF  |
|--------------|-------------|-------------|--------|---------|-----|
| Input        | 28×28       | —           | —      | —       | 1   |
| Conv2d-1     | 26×26       | 3×3         | 1      | 0       | 3   |
| Conv2d-5     | 24×24       | 3×3         | 1      | 0       | 5   |
| Conv2d-9     | 24×24       | 1×1         | 1      | 0       | 5   |
| MaxPool2d-13 | 12×12       | 2×2         | 2      | 0       | 6   |
| Conv2d-14    | 10×10       | 3×3         | 1      | 0       | 10  |
| Conv2d-18    | 8×8         | 3×3         | 1      | 0       | 14  |
| Conv2d-22    | 6×6         | 3×3         | 1      | 0       | 18  |
| Conv2d-26    | 6×6         | 3×3         | 1      | 0       | 18  |
| AvgPool2d-30 | 1×1         | 6×6         | 6      | 0       | 28  |
| Conv2d-31    | 1×1         | 1×1         | 1      | 0       | 28  |

---

### **Net3 Receptive Field Table**
| Layer            | Output Size | Kernel Size | Stride | Padding | RF  |
|-------------------|-------------|-------------|--------|---------|------|
| ConvBlock1       | 26x26       | 3x3         | 1      | 0       | 3    |
| ConvBlock2       | 24x24       | 3x3         | 1      | 0       | 5    |
| Pooling          | 12x12       | 2x2         | 2      | 0       | 6    |
| Transition1      | 12x12       | 1x1         | 1      | 0       | 6    |
| ConvBlock3       | 10x10       | 3x3         | 1      | 0       | 10   |
| ConvBlock3-2     | 8x8         | 3x3         | 1      | 0       | 14   |
| ConvBlock3-3     | 6x6         | 3x3         | 1      | 0       | 18   |
| GAP              | 1x1         | 6x6         | 1      | 0       | 28   |
| ConvBlock5       | 1x1         | 1x1         | 1      | 0       | 28   |

Each table provides a breakdown of the output size, kernel size, stride, padding, and receptive field size for every layer in the respective networks.

# Best Model Paramters (99.43 Test Accuracy)

```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 8, 26, 26]              72
              ReLU-2            [-1, 8, 26, 26]               0
       BatchNorm2d-3            [-1, 8, 26, 26]              16
           Dropout-4            [-1, 8, 26, 26]               0
            Conv2d-5           [-1, 16, 24, 24]           1,152
              ReLU-6           [-1, 16, 24, 24]               0
       BatchNorm2d-7           [-1, 16, 24, 24]              32
           Dropout-8           [-1, 16, 24, 24]               0
         MaxPool2d-9           [-1, 16, 12, 12]               0
           Conv2d-10            [-1, 8, 12, 12]             128
             ReLU-11            [-1, 8, 12, 12]               0
      BatchNorm2d-12            [-1, 8, 12, 12]              16
           Conv2d-13           [-1, 12, 10, 10]             864
             ReLU-14           [-1, 12, 10, 10]               0
      BatchNorm2d-15           [-1, 12, 10, 10]              24
          Dropout-16           [-1, 12, 10, 10]               0
           Conv2d-17             [-1, 16, 8, 8]           1,728
             ReLU-18             [-1, 16, 8, 8]               0
      BatchNorm2d-19             [-1, 16, 8, 8]              32
          Dropout-20             [-1, 16, 8, 8]               0
           Conv2d-21             [-1, 20, 6, 6]           2,880
             ReLU-22             [-1, 20, 6, 6]               0
      BatchNorm2d-23             [-1, 20, 6, 6]              40
          Dropout-24             [-1, 20, 6, 6]               0
        AvgPool2d-25             [-1, 20, 1, 1]               0
           Conv2d-26             [-1, 16, 1, 1]             320
             ReLU-27             [-1, 16, 1, 1]               0
      BatchNorm2d-28             [-1, 16, 1, 1]              32
          Dropout-29             [-1, 16, 1, 1]               0
           Conv2d-30             [-1, 10, 1, 1]             160
================================================================
Total params: 7,496
Trainable params: 7,496
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.58
Params size (MB): 0.03
Estimated Total Size (MB): 0.61

----------------------------------------------------------------

----------------------------------------------------------------
Training Logs
----------------------------------------------------------------
EPOCH: 0
Loss=0.07109811902046204 Batch_id=468 Accuracy=93.00: 100%|██████████| 469/469 [00:13<00:00, 35.85it/s] 

Test set: Average loss: 0.0489, Accuracy: 9848/10000 (98.48%)

EPOCH: 1
Loss=0.11327752470970154 Batch_id=468 Accuracy=97.80: 100%|██████████| 469/469 [00:13<00:00, 35.52it/s] 

Test set: Average loss: 0.0395, Accuracy: 9872/10000 (98.72%)

EPOCH: 2
Loss=0.01554503757506609 Batch_id=468 Accuracy=98.26: 100%|██████████| 469/469 [00:13<00:00, 36.08it/s] 

Test set: Average loss: 0.0306, Accuracy: 9903/10000 (99.03%)

EPOCH: 3
Loss=0.021954407915472984 Batch_id=468 Accuracy=98.44: 100%|██████████| 469/469 [00:13<00:00, 35.76it/s] 

Test set: Average loss: 0.0303, Accuracy: 9908/10000 (99.08%)

EPOCH: 4
Loss=0.04818737506866455 Batch_id=468 Accuracy=98.64: 100%|██████████| 469/469 [00:13<00:00, 36.04it/s]  

Test set: Average loss: 0.0268, Accuracy: 9919/10000 (99.19%)

EPOCH: 5
Loss=0.02145584672689438 Batch_id=468 Accuracy=98.70: 100%|██████████| 469/469 [00:12<00:00, 36.18it/s]  

Test set: Average loss: 0.0222, Accuracy: 9929/10000 (99.29%)

EPOCH: 6
Loss=0.0078322384506464 Batch_id=468 Accuracy=98.82: 100%|██████████| 469/469 [00:12<00:00, 36.21it/s]   

Test set: Average loss: 0.0272, Accuracy: 9919/10000 (99.19%)

EPOCH: 7
Loss=0.004873286932706833 Batch_id=468 Accuracy=98.89: 100%|██████████| 469/469 [00:13<00:00, 36.08it/s] 

Test set: Average loss: 0.0238, Accuracy: 9927/10000 (99.27%)

EPOCH: 8
Loss=0.019541041925549507 Batch_id=468 Accuracy=99.01: 100%|██████████| 469/469 [00:12<00:00, 36.68it/s] 

Test set: Average loss: 0.0223, Accuracy: 9940/10000 (99.40%)

EPOCH: 9
Loss=0.016221312806010246 Batch_id=468 Accuracy=99.00: 100%|██████████| 469/469 [00:12<00:00, 36.80it/s] 

Test set: Average loss: 0.0247, Accuracy: 9918/10000 (99.18%)

EPOCH: 10
Loss=0.022381002083420753 Batch_id=468 Accuracy=99.05: 100%|██████████| 469/469 [00:12<00:00, 37.21it/s] 

Test set: Average loss: 0.0236, Accuracy: 9928/10000 (99.28%)

EPOCH: 11
Loss=0.03846469148993492 Batch_id=468 Accuracy=99.05: 100%|██████████| 469/469 [00:12<00:00, 36.99it/s]  

Test set: Average loss: 0.0201, Accuracy: 9943/10000 (99.43%)

EPOCH: 12
Loss=0.008482008241117 Batch_id=468 Accuracy=99.11: 100%|██████████| 469/469 [00:12<00:00, 36.33it/s]    

Test set: Average loss: 0.0236, Accuracy: 9929/10000 (99.29%)

EPOCH: 13
Loss=0.010355763137340546 Batch_id=468 Accuracy=99.13: 100%|██████████| 469/469 [00:13<00:00, 35.82it/s] 

Test set: Average loss: 0.0228, Accuracy: 9926/10000 (99.26%)

EPOCH: 14
Loss=0.12619204819202423 Batch_id=468 Accuracy=99.17: 100%|██████████| 469/469 [00:13<00:00, 34.11it/s]  

Test set: Average loss: 0.0243, Accuracy: 9926/10000 (99.26%)
```
![Training GIF](./training_gif_aws.gif)

