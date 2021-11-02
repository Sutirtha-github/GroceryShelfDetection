

Dataset Preparation:

\1. Download the ShelfImages dataset and untar it.

\2. The data has already been split into train/test here.

\3. Annotations are provided in a single ﬁle as annotations.txt in gulvarol/grocerydataset

repository. The format of the given annotations are:

x\_center<i> y\_center<i> box\_width<i> box\_height<i> class<i> …

YOLOv5 demands normalized annotations of the following format:

class<i> x\_center<i>/img\_width y\_center<i>/img\_height box\_width<i>/img\_width

box\_height<i>/img\_height

…

Create individual annotation ﬁles for each image in their corresponding folder. It should look

something like this:

train/

Img1.jpg

Img1.txt

Img2.jpg

Img2.txt

…

test/

Img3.jpg

Img3.txt

Img4.jpg

Img.txt

…

\4. Now clone the ultralytics/yolov5 repository and create the following three ﬁles inside

the yolov5 folder:

●

●

●

dataset.yaml

Training.txt

validation.txt

\5. Write the paths of individual ﬁles of training data(.jpg+.txt) and test data(.jpg+.txt) inside

training.txt and validation.txt respectively.

dataset.yaml will contain:

●

●

●

●

●

Path to dataset folder

Path of training.txt

Path of validation.txt

Number of classes (=11 here)

Names of each class like ‘marlboro’, ‘monte carlo’ etc.

Augmentations:





Mosaic technique is used for data augmentation in yolov5. Four small pictures are

assembled into a large picture, and the four small pictures are randomly processed during splicing,

so the size and shape of the four small pictures are different. Following are the visuals of mosaic

augmentations on our dataset

Detection Network:

Pre-trained yolov5m6.pt has been used for training. It has 35.7 M parameters, 50.0 B FLOPs

@640, size 68.7 MB. COCO mAPval 0.5 is 69.0 and mAPval 0.5:0.95 is 51.0.

Training Parameters:

nc: 11 # number of classes

depth\_multiple: 0.67 # model depth multiple

width\_multiple: 0.75 # layer channel multiple

Hyperparameters:

lr0: 0.01 # initial learning rate (SGD=1E-2, Adam=1E-3)

lrf: 0.2 # ﬁnal OneCycleLR learning rate (lr0 \* lrf)

momentum: 0.937 # SGD momentum/Adam beta1

weight\_decay: 0.0005 # optimizer weight decay 5e-4





warmup\_epochs: 3.0 # warmup epochs (fractions ok)

warmup\_momentum: 0.8 # warmup initial momentum

warmup\_bias\_lr: 0.1 # warmup initial bias lr

box: 0.05 # box loss gain

cls: 0.3 # cls loss gain

cls\_pw: 1.0 # cls BCELoss positive\_weight

obj: 0.7 # obj loss gain (scale with pixels)

obj\_pw: 1.0 # obj BCELoss positive\_weight

iou\_t: 0.20 # IoU training threshold

anchor\_t: 4.0 # anchor-multiple threshold

\# anchors: 3 # anchors per output layer (0 to ignore)

ﬂ\_gamma: 0.0 # focal loss gamma (eﬃcientDet default gamma=1.5)

hsv\_h: 0.015 # image HSV-Hue augmentation (fraction)

hsv\_s: 0.7 # image HSV-Saturation augmentation (fraction)

hsv\_v: 0.4 # image HSV-Value augmentation (fraction)

degrees: 0.0 # image rotation (+/- deg)

translate: 0.1 # image translation (+/- fraction)

scale: 0.9 # image scale (+/- gain)

shear: 0.0 # image shear (+/- deg)

perspective: 0.0 # image perspective (+/- fraction), range 0-0.001

ﬂipud: 0.0 # image ﬂip up-down (probability)

ﬂiplr: 0.5 # image ﬂip left-right (probability)

mosaic: 1.0 # image mosaic (probability)

mixup: 0.1 # image mixup (probability)

copy\_paste: 0.1 # segment copy-paste (probability)

Anchor box:

\- [10,13, 16,30, 33,23] # P3/8

\- [30,61, 62,45, 59,119] # P4/16

\- [116,90, 156,198, 373,326] # P5/32

