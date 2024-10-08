# Chess_Recognition-and-FEN
**Root Directory**
```
Chess
├─icon
├─images
├─model
```
- **`model` Directory**

`rename.py` is optional, used for renaming the images.

`Data_Aug.py` is optional, used for data augmentation. Referrence: https://blog.csdn.net/qq_38973721/article/details/128700920

`add_Data.py` is optional, user for add images from other folders. 

`dataloader.py` overwrites the `Dataset` class for this dataset. 

`model.py` is the network architecture, employing modules from `modules.py`. This network fine-tuned the ResNet50. The architecture can be seen in the figure 1. 
![resnet](https://github.com/user-attachments/assets/22d811c6-53fb-484d-bfba-0142c07532a2)

`train.py` and `valid.py` is used for training the test the model. 
> This project used `channels = 1` to train the model to improve the recognition accuracy for black and white pieces. It's curious that the fine-tuned ResNet has poor performance to distinguish the black and white. I has tried to turn the images to the gray images with 3 channels. Compared with the grey image with single channel, the 3-channel images has no ability to recognize the black and white pieces. I'm curious about this phenomenon. 

`recognize.py` contains the function of the chessboard division into `8*8` pieces for recognition by caliing the `Board` class from `read_contour.py` to get the square chessboard. Load the training weight and generate the recognition results. 

`Compare.py` is used to generate changes in the state of the chessboard before and after. 

--------------------------------------------------------------

`rename.py` 是可选的，用于重命名图像。

`Data_Aug.py` 是可选的，用于数据增强。参考：https://blog.csdn.net/qq_38973721/article/details/128700920

`add_Data.py` 是可选的，用户用于从其他文件夹添加图像。

`dataloader.py` 覆盖此数据集的 `Dataset` 类。

`model.py`是网络架构，使用`modules.py`中的模块。该网络对 ResNet50 进行了微调。其架构如图1所示。

`train.py` 和 `valid.py` 用于训练和测试模型。
> 本项目使用`channels = 1`来训练模型，以提高黑白棋子的识别精度。奇怪的是，经过微调的 ResNet 在区分黑白方面的性能很差。我尝试将RGB图像转换为具有 3 个通道的灰色图像。与单通道的灰度图像相比，三通道图像不具备识别黑白棋子的能力。我很不理解。

`recognize.py`包含将棋盘分割成`8*8`块进行识别的功能，通过调用`read_contour.py`中的`Board`类得到正方形棋盘。加载训练权重并生成识别结果。

`Compare.py` 用于生成前后棋盘状态的变化。

```
棋盘数组为:[[0, 12, 2, 4, 12, 2, 12, 12], [5, 5, 12, 12, 1, 5, 12, 0], [1, 12, 12, 12, 12, 12, 12, 5], [12, 7, 5, 12, 11, 12, 5, 12], [12, 12, 12, 12, 12, 11, 11, 12], [12, 12, 12, 12, 11, 12, 12, 8], [11, 11, 12, 12, 12, 12, 12, 11], [6, 12, 8, 10, 12, 12, 7, 6]]
具体棋盘为:[['rook', ' ', 'bishop', 'king', ' ', 'bishop', ' ', ' '], ['soldier', 'soldier', ' ', ' ', 'knight', 'soldier', ' ', 'rook'], ['knight', ' ', ' ', ' ', ' ', ' ', ' ', 'soldier'], [' ', 'KNIGHT', 'soldier', ' ', 'SOLDIER', ' ', 'soldier', ' '], [' ', ' ', ' ', ' ', ' ', 'SOLDIER', 'SOLDIER', ' '], [' ', ' ', ' ', ' ', 'SOLDIER', ' ', ' ', 'BISHOP'], ['SOLDIER', 'SOLDIER', ' ', ' ', ' ', ' ', ' ', 'SOLDIER'], ['ROOK', ' ', 'BISHOP', 'KING', ' ', ' ', 'KNIGHT', 'ROOK']]
棋盘数组为:[[0, 12, 12, 4, 12, 2, 12, 12], [5, 5, 12, 12, 1, 5, 12, 0], [1, 12, 12, 12, 12, 12, 12, 5], [12, 7, 5, 12, 11, 12, 5, 12], [12, 12, 12, 12, 12, 11, 2, 12], [12, 12, 12, 12, 11, 12, 12, 8], [11, 11, 12, 12, 12, 12, 12, 11], [6, 12, 8, 10, 12, 12, 7, 6]]
具体棋盘为:[['rook', ' ', ' ', 'king', ' ', 'bishop', ' ', ' '], ['soldier', 'soldier', ' ', ' ', 'knight', 'soldier', ' ', 'rook'], ['knight', ' ', ' ', ' ', ' ', ' ', ' ', 'soldier'], [' ', 'KNIGHT', 'soldier', ' ', 'SOLDIER', ' ', 'soldier', ' '], [' ', ' ', ' ', ' ', ' ', 'SOLDIER', 'bishop', ' '], [' ', ' ', ' ', ' ', 'SOLDIER', ' ', ' ', 'BISHOP'], ['SOLDIER', 'SOLDIER', ' ', ' ', ' ', ' ', ' ', 'SOLDIER'], ['ROOK', ' ', 'BISHOP', 'KING', ' ', ' ', 'KNIGHT', 'ROOK']]
['c8 -> g4']
```
`FEN.py` is **imcomplete**, used for converting the chessboard data into FEN string. 
- **Dataset Directory**

All the images are divided into 13 classes, representing 12 types of pieces and empty status. Images are collected from the [`chess.com`](https://www.chess.com/) screenshots.  

所有图像分为13类，代表12种棋子和空状态。图片是从“chess.com”屏幕截图中收集的。

`Origin` folder stores the original images.

`Rename` folder stores the renamed images.  

`ImageDataset` folder stores the training image data after Dataset Augmentation: `./model/Data_Aug`.  

`valid_ImageDataset` stores the test image data.  
```
├─ImageDataset
│  ├─00rook black
│  ├─01knight black
│  ├─02bishop black
│  ├─03queen black
│  ├─04king black
│  ├─05sodier black
│  ├─06rook white
│  ├─07knight white
│  ├─08bishop white
│  ├─09queen white
│  ├─10king white
│  ├─11sodier white
│  └─12empty
├─Origin
│  ├─...
├─Rename
│  ├─...
└─valid_ImageDataset
```
All the datasets the training weight (.pth) can be downloaded from:

**BaiduNetDisk**

URL:https://pan.baidu.com/s/1gI27GXrSjcB9CejoJAcN0w?pwd=qhzv 

CODE: qhzv

***Note that the `new2.py` contains some methods to crawl web data: ["chess.com"](https://www.chess.com/). Instead of using conventional mathods, I screenshot some icon images and write a program to achieve icon matching and then implement multiple functions. This is a half-effort idea, but subject to company requirements, I have to do this.***
