# Bottom try on

## Data preprocessing

We convert the original data [VITON](https://github.com/xthan/VITON) into different directories for easily use. 


You can get the processed data at [GoogleDrive](https://drive.google.com/file/d/1la2eVSJz-ZCgG4KlL5o4gUvJIp9lXGCk/view?usp=sharing) or by running:

## Geometric Matching Module

### training
We just use L1 loss for criterion in this code. 

TV norm constraints for the offsets will make GMM more robust.

An example training command is
```
python train.py --name gmm_train_new --stage GMM --workers 4 --save_count 5000 --shuffle
```


### eval

Choose the different source data for eval with the option ```--datamode```.

An example training command is
```
python test.py --name gmm_traintest_new --stage GMM --workers 4 --datamode test --data_list test_pairs.txt --checkpoint checkpoints/gmm_train_new/gmm_final.pth
```

You can see the results in tensorboard, as show below.

## Try-On Module
### background keep
Using `cp_dataset.py` for keep background and `cp_dataset_old` for remove background 
### training
Before the trainning, you should generate warp-mask & warp-cloth, using the test process of GMM with `--datamode train`. 
Then move these files or make soft links under the directory `data/train`.
An example training command is

```
python train.py --name tom_train_new --stage TOM --workers 4 --save_count 5000 --shuffle 
```
You can see the results in tensorboard, as show below.



### eavl
An example training command is

```
python test.py --name tom_test_new --stage TOM --workers 4 --datamode test --data_list test_pairs.txt --checkpoint checkpoints/tom_train_new/tom_final.pth
```

You can see the results in tensorboard, as show below.
## Pretrain model
You can download [here](https://drive.google.com/drive/folders/1lfDS6AHXymMWzJ_5NoPPTiy5iGiFr2EE?usp=sharing)