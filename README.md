
# AI引擎接入文档

## 应用介绍

AI引擎平台是面向人工智能研究中的数据处理、模型训练等各个流程的技术难点研发的数据可视化平台，为用户提供一站式算法管理、便利的模型训练和实时的日志反馈，可节省训练成本和时间，小白用户亦可一键上手。

## 主要功能：

### 1.用户权限体系

### 2.模型上传

### 3.数据集上传

### 4.数据存储

### 5.一键训练

### 6.算法运行支撑

### 7.日志打印

#### 应用权限

调用AI引擎时，离不开调用服务端接口，这些操作会访问用户，操作用户的信息。在实际使用过程中，应用需要申请资源访问的权限，并经过开放平台
权限列表

| 权限名称     | 权限说明                             | 关联API/事件                         |
| ------------ | ------------------------------------ | ------------------------------------ |
| 权限模组     |                                      |                                      |
| 获取用户信息 | 获得用户读取权限，可查询个人基础信息 | 批量获取用户获取用户详情获取用户列表 |
| 更新用户信息 | 针对个人当前基础属性更新             | 修改用户部分信息更新用户所有信息     |
| 获取角色列表 | 获取当前角色列表                     | 批量获取当前组的角色列表             |
| 获取角色属性 | 获取当前指定角色的属性               | 获取指定角色的基本属性               |
| 创建用户     | 创建用户                             | 创建用户                             |

| 名称             | 说明                                                         | 关联API/事件                               |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------ |
| 模型模组         |                                                              |                                            |
| 上传模型         | 定义模型信息和名称                                           | 批量获取模型信息批量插入模型信息           |
| 更新模型         | 对模型当前的基础属性更新                                     | 更新模型信息                               |
| 算法回调模型接口 | 算法训练完后会对模型进行回调，修改模型状态为可训练状态，并关闭读取文件的流 | 获取模型信息模型数据更新                   |
| 获取模型属性列表 | 获取符合规定条件的模型属性                                   | 批量获取模型信息                           |
| 一键训练         | 根据模型名称对模型进行训练                                   | 一键训练获取模型信息获取数据集信息调用算法 |

| 名称               | 说明                           | 关联API/事件                             |
| ------------------ | ------------------------------ | ---------------------------------------- |
| 数据集模组         |                                |                                          |
| 初始化数据集       | 上传数据集的文件和定义字段属性 | 获取用户信息初始化文件列表保存数据集信息 |
| 更新数据集         | 对数据集当前的基础属性更新     | 查询数据集信息更新数据集信息             |
| 获取数据据属性列表 | 获取符合规定条件的数据集属性   | 批量获取数据集信息                       |

#### 模型上传

用户将准备好的模型zip压缩文档在创建模型时进行上传，在界面上自定义好模型名称、版本、模型类型等关键数据字段

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficModel/insert](http://localhost:6083/roadDetectionV2/highSpeedTrafficModel/insert) |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）

[

{

​    "version": "v1.0",

​    "modelName": "pictureAnalyzeModel",

​    "modelType": 0

}

]

### 返回值（json）

{

​    "bucketName": "4eff8f27-3db9-458a-930b-1e8f774bb098"

}

#### 数据集上传

用户将准备好的数据集zip压缩文档在创建数据集页面进行上传，需要关联对应的算法模型

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficUpload/](http://localhost:6083/roadDetectionV2/highSpeedTrafficUpload/)initDataset |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）

[

​    {

​        "fileSize": "1024",

​        "modelId": "123456789",

​        "modelName": "pictureAnalyzeModel",

​        "bucketName": "4eff8f27-3db9-458a-930b-1e8f774bb098",

​        "datasetName": "ceshi",

​        "filenames": [

​            "apple",

​            "banana",

​            "orange"

​        ],

​        "filename":"summaryFile"

​    }

]

### 返回值

true or false

#### 更新数据集

将已上传的数据集做更新操作，修正信息等

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficUpload/](http://localhost:6083/roadDetectionV2/highSpeedTrafficUpload/)updateDataset |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）

[

​    {

​        "datasetId": "1024",

​        "fileName": "123456789",

​    }

]

### 返回值

true or false

#### 获取数据集列表

获取所有已经上传过的数据集列表

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficUpload/](http://localhost:6083/roadDetectionV2/highSpeedTrafficUpload/)getSourceDatasetList |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）

[

​    {

​        "currentPage": "1",

​        "limit": "10

​    }

]

### 返回值

{    **"bucketName"**:**null**,    **"datasetId"**:**null**,    **"datasetName"**:**null**,    **"datasetContent"**:**null**,    **"fileSize"**:**null**,    **"gmtCreated"**:**null**,    **"gmtModified"**:**null**,    **"id"**:**null**,    **"isDeleted"**:**null**,    **"modelName"**:**null**,    **"modelId"**:**null**,    **"ownerId"**:**null**,    **"ownerName"**:**null**,    **"status"**:**null**,    **"totalNumber"**:**null**,    **"uploadNumber"**:**null** }

#### 模型更新

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficModel/](http://localhost:6083/roadDetectionV2/highSpeedTrafficModel/)update |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）（是根据modelName字段进行数据的索引，所以入参一定要有modelName）

{

​    "version": "v2.0",

​    "modelName": "pictureAnalyzeModel",

​    "modelType": 1,

​    "fileName": "mnist.zip"

}

### 返回值

true

#### 算法回调模型接口

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficModel/](http://localhost:6083/roadDetectionV2/highSpeedTrafficModel/)getModelList |
| HTTP Method | POST                                                         |

无需请求头

### 请求体（json）

{

​    "modelName": "pictureAnalyzeModel"

}

### 返回值

true

#### 获取模型列表

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficModel/](http://localhost:6083/roadDetectionV2/highSpeedTrafficModel/)update |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）

{}

### 返回值

[

​    {

​        "id": 8,

​        "modelId": 1684201790420,

​        "version": "v111",

​        "modelName": "mnist",

​        "bucketName": "alg",

​        "modelTrainCommand": "docker build xxx",

​        "isDeleted": 0,

​        "modelType": 1,

​        "modelStatus": 0,

​        "importStatus": 0,

​        "gmtCreated": "2023-05-15 17:18:02",

​        "gmtImported": 0,

​        "gmtModified": "2023-05-15 17:18:02",

​        "fileName": "mnist.tar",

​        "logPath": "/home/lbw/project/AI-engine/train/mnist/log/0.log"

​    }

]

#### 一键训练

用户点击模型训练按钮，会在后台对模型进行训练，训练过程中按钮不可再次点击，训练结束后后台会返回并显示模型训练的精度结果。同时也支持将使用不同的测试数据集对训练好的模型进行精度评估。

### 请求

| 基本        |                                                              |
| ----------- | ------------------------------------------------------------ |
| HTTP URL    | [localhost:6083/roadDetectionV2/highSpeedTrafficModel/](http://localhost:6083/roadDetectionV2/highSpeedTrafficModel/)modelTrain |
| HTTP Method | POST                                                         |

### 请求头

| 名称         | 类型   | 必填 | 描述                                                         |
| ------------ | ------ | ---- | ------------------------------------------------------------ |
| X-Auth-Token | string | 是   | 权限系统返回的token 示例值：486f4b68-b224-468d-8fce-995c490a520b |

### 请求体（json）

[

​    {

​        "modelName": "mnist"

​    }

]

### 图像分类任务一键训练

#### 图像分类数据集

数据集主路径下需包含一个数据集配置文件config.yaml，并划分为train、valid、test三个二级路径，其中train与valid不得为空路径。每个子路径下包含images三级路径及labels.txt标注数据，images路径下存放图片数据（统一为jpg或png格式），各二级路径下所有图片数据与标注数据命名需一一对应。数据集路径示例如下：

```Plain
# 带*标记的用户可自行命名
--data*
  └-config.yaml
  └-train
    └-images
      └-pic00*.jpg
      └-pic01*.jpg
      └-...
    └-labels.txt
  └-valid
    └-images
      └-...
    └-labels.txt
  └-test
    └-images
      └-...
    └-labels.txt
```

其中数据集配置文件config.yaml示例如下，需符合yaml格式，nc为数据集中所标注图片的总类别数，names为数据集中所标注物体的命名：

```Plain
# 类别数量
nc: 29
# 类别名
names: ["amphibian", "animal", "appliance", "bird", "covering", "device", "fabric", 
        "fish", "flower", "food", "fruit", "fungus", "furniture", "geological", 
        "formation", "invertebrate", "mammal", "musical", "instrument", "plant", 
        "reptile", "sport", "structure", "tool", "tree", "utensil", "vegetable", 
        "vehicle", "person"]
```

标注数据示例如下，每行代表图片所标记类别，格式为"pic_name  cls_id"，pic_name为图片名，cls_id为物体类别ID（需遵照config.yaml）。

```Plain
pic00*  1
pic01*  5
...
```

#### 图像分类训练

模型训练所需的环境及脚本需打包入docker镜像，并附带模型接口配置文件config.yaml。训练容器开启后数据集将映射至容器内的/home/mapping路径下，并统一更名为data，data路径下的结构与“图像分类数据集”中描述一致。训练得到的模型权重文件及日志需输出到容器的/home/mapping/ckpt路径下，如/home/mapping/ckpt/train.pth和/home/mapping/ckpt/train.log。开发者需预先对脚本做好配置。

模型接口配置文件config.yaml中需说明模型名称、任务类型信息、训练入参及默认值并附带说明、训练启动命令、验证入参及默认值并附带说明、验证启动命令等。

```Bash
# 模型名称
model: 'xxx'
# 任务类型信息
task: 'classify'
nc: 10
names: ["amphibian", "animal", "appliance", "bird", "covering", "device", "fabric", 
        "fish", "flower", "food"]
        
# 训练入参
tra_params: {batch_size: 16, optimizer: 'SGD'...}
# 训练入参说明：batch_size批次大小，optimizer优化器类型
# 训练启动命令
tra_coda: "conda activate myEnv && cd /home/Project && python train.py --batch_size 16  --optimizer 'SGD' ..."

# 验证入参
val_params: {ckpt_path: '/home/mapping/ckpt/train.pth' ...}
# 验证入参说明：ckpt_path模型文件路径
# 验证启动命令
val_coda: "conda activate myEnv && cd /home/Project && python valid.py --ckpt_path '/home/mapping/ckpt/train.pth' ..."
```

| 变量名     | 类型 | 备注                                     |
| ---------- | ---- | ---------------------------------------- |
| model      | str  | 必需，模型名称                           |
| task       | str  | 必需，任务类型，分类模型统一填'classify' |
| nc         | int  | 必需，分类模型类别总数                   |
| names      | list | 必需，分类模型类别细分                   |
| tra_params | obj  | 必需，训练入参及默认值                   |
| tra_coda   | str  | 必需，训练启动命令                       |
| val_params | obj  | 必需，验证入参及默认值                   |
| val_coda   | str  | 必需，验证启动命令                       |

### 物体检测模型一键训练

#### 物体检测数据集

数据集主路径下需包含一个数据集配置文件config.yaml，并划分为train、valid、test三个二级路径，其中train与valid不得为空路径。每个子路径下包含images三级路径及labels.txt标注数据，images路径下存放图片数据（统一为jpg或png格式），各二级路径下所有图片数据与标注数据命名需一一对应。数据集路径示例如下：

```Plain
# 带*标记的用户可自行命名
--data*
  └-config.yaml
  └-train
    └-images
      └-pic00*.jpg
      └-pic01*.jpg
      └-...
    └-labels
      └-pic00*.txt
      └-pic01*.txt
      └-...
  └-valid
    └-images
      └-...
    └-labels
      └-...
  └-test
    └-images
      └-...
    └-labels
      └-...
```

其中数据集配置文件config.yaml示例如下，需符合yaml格式，nc为数据集中所标注图片的总类别数，names为数据集中所标注物体的命名：

```Plain
# 类别数量
nc: 80
# 类别名
names: ["person", "bicycle", "car", "motorcycle", "airplane", "bus", "train", "truck", 
"boat", "traffic light", "fire hydrant", "stop sign", "parking meter", "bench", "bird", 
"cat", "dog", "horse", "sheep", "cow", "elephant", "bear", "zebra", "giraffe", "backpack", 
"umbrella", "handbag", "tie", "suitcase", "frisbee", "skis", "snowboard", "sports ball", 
"kite", "baseball bat", "baseball glove", "skateboard", "surfboard", "tennis racket", 
"bottle", "wine glass", "cup", "fork", "knife", "spoon", "bowl", "banana", "apple", 
"sandwich", "orange", "broccoli", "carrot", "hot dog", "pizza", "donut", "cake", "chair", 
"couch", "potted plant", "bed", "dining table", "toilet", "tv", "laptop", "mouse", 
"remote", "keyboard", "cell phone", "microwave", "oven", "toaster", "sink", "refrigerator", 
"book", "clock", "vase", "scissors", "teddy bear", "hair drier", "toothbrush"]
```

标注数据示例如下，每行代表图片中所标记的一个物体选框，格式为"cls_id  r_c_x  r_c_y  r_w  r_h"。cls_id为物体类别ID（参照config.yaml）；r_c_x、r_c_y分别为选框中心坐标(c_x, c_y)于图片宽高(W, H)的相对值：r_c_x = c_x/W，r_c_y = c_y/H；r_w、r_h分别为选框宽高(w, h)于图片宽高(W, H)的相对值：r_w = w/W, r_h = h/H。

```Plain
3  0.5433593750 0.2884259259 0.0200520833 0.0435185185
21 0.4559895833 0.3125000000 0.0098958333 0.1324074074
21 0.4248697917 0.2773148148 0.0122395833 0.2083333333
17 0.6247395833 0.4638888889 0.0046875000 0.0314814815
6  0.3833333333 0.1898148148 0.0489583333 0.1333333333
6  0.5296875000 0.3162037037 0.0130208333 0.0324074074
3  0.5981770833 0.1166666667 0.0640625000 0.2018518519
3  0.5186197917 0.3356481481 0.0117187500 0.0361111111
8  0.4875000000 0.4236111111 0.0213541667 0.0935185185
...
```

#### 物体检测训练

模型训练所需的环境及脚本需打包入docker镜像，并附带模型接口配置文件config.yaml。训练容器开启后数据集将映射至容器内的/home/mapping路径下，并统一更名为data，data路径下的结构与“物体检测数据集”中描述一致。训练得到的模型权重文件及日志需输出到容器的/home/mapping/ckpt路径下，如/home/mapping/ckpt/train.pth和/home/mapping/ckpt/train.log。开发者需预先对脚本做好配置。

模型接口配置文件config.yaml中需说明模型名称、任务类型信息、训练入参及默认值并附带说明、训练启动命令、验证入参及默认值并附带说明、验证启动命令等。

```Bash
# 模型名称
model: 'xxx'
# 任务类型信息
task: 'detect'
nc: 10
names: ["person", "bicycle", "car", "motorcycle", "airplane", "bus", "train", "truck", 
        "boat", "traffic light"]
        
# 训练入参
tra_params: {batch_size: 16, optimizer: 'ADAM'...}
# 训练入参说明：batch_size批次大小，optimizer优化器类型
# 训练启动命令
tra_coda: "conda activate myEnv && cd /home/Project && python train.py --batch_size 16  --optimizer 'ADAM' ..."

# 验证入参
val_params: {ckpt_path: '/home/mapping/ckpt/train.pth' ...}
# 验证入参说明：ckpt_path模型文件路径
# 验证启动命令
val_coda: "conda activate myEnv && cd /home/Project && python valid.py --ckpt_path '/home/mapping/ckpt/train.pth' ..."
```

| 变量名     | 类型 | 备注                                       |
| ---------- | ---- | ------------------------------------------ |
| model      | str  | 必需，模型名称                             |
| task       | str  | 必需，任务类型，物体检测模型统一填'detect' |
| nc         | int  | 必需，分类模型类别总数                     |
| names      | list | 必需，分类模型类别细分                     |
| tra_params | obj  | 必需，训练入参及默认值                     |
| tra_coda   | str  | 必需，训练启动命令                         |
| val_params | obj  | 必需，验证入参及默认值                     |
| val_coda   | str  | 必需，验证启动命令                         |

#### 数据存储

用户上传的模型的时候会进行minio的桶创建，每一个模型对应一个bucket，同时创建完模型数据后会数据集会统一存储到minio文件系统里，可以通过查询桶名称查看和下载对应文件

#### 日志打印

用户点击一键训练以后，会实时打印出训练日志，后台通过webSocket把日志信息发送到前端进行展示