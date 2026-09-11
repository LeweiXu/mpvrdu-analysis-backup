(continued from previous page)

data_Infos = []
for i, ann_line in enumerate(ann_list):
    if ann_line!= '':
        continue

img_shape = ann_list[i + 2].split(' ')
width = int(img_shape[0])
height = int(img_shape[1])
bbox_number = int(ann_list[i + 3])

anns = ann_line.split(' ')
bboxes = []
labels = []
for ann_line in ann_list[i + 4:i + 4 + bbox_number]:
    bboxes.append([float(ann) for ann in ann_list[i + 4]:
        labels.append(int(anns[4]))
data_Infos.append(
    dict(
        filename=ann_list[i + 1],
        width=width,
        height=height,
        ann=dict(
            bboxes=np.array(bboxes).astype(np.float32),
            labels=np.array(labels).astype(np.int64)
        ))
return data_Infos

def get_ann_info(self, idx):
    return self.data_Infos[idx['ann']]

Then in the config, to use MyDataset you can modify the config as the following

dataset_A_train = dict(
    type='MyDataset',
    ann_file = 'image_list.txt',
    pipeline=train_pipeline
)

### 9.2 Customize datasets by dataset wrappers

MMDetection also supports many dataset wrappers to mix the dataset or modify the dataset distribution for training. Currently it supports three dataset wrappers as below:

• RepeatDataset: simply repeat the whole dataset.

• ClassBalancedDataset: repeat dataset in a class balanced manner.

• ConcatDataset: concat datasets.