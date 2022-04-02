# yujie_eval_notes

## env

> please refer to <https://github.com/hibetterheyj/DenseMatch4VOS/tree/master/cfg>

```shell
conda install scikit-learn
python -m pip install wandb
```

## test

- Label Propagation

```shell
cd code
# python test.py --filelist /path/to/davis/vallist.txt \
# --model-type scratch --resume ../pretrained.pth --save-path /save/path \
# --topk 10 --videoLen 20 --radius 12  --temperature 0.05  --cropSize -1

# modified
python test.py --model-type scratch --resume ../pretrained.pth --save-path ./results \
--topk 10 --videoLen 20 --radius 12  --temperature 0.05  --cropSize -1
```

### res

#### only run first test

```shell
...
computing resized lbl for //home/he/data/davis/Annotations/480p/blackswan/00048_size60x107.npy
computing onehot lbl for //home/he/data/davis/Annotations/480p/blackswan/00049_onehot.npy
computing resized lbl for //home/he/data/davis/Annotations/480p/blackswan/00049_size60x107.npy
******* Vid 1 (70 frames) *******
computed features 1.143826961517334
...
computing affinity
155.64102363586426 affinity forward, max mem 1157.48095703125
******* Vid 0 TOOK 168.2065885066986 *******
******* Vid 1 - blackswan (70 frames) *******
Killed
```

#### start from bmx-trees

```shell
******* Vid 0 - bmx-trees (100 frames) *******
computing affinity
159.54543924331665 affinity forward, max mem 1128.580078125
Traceback (most recent call last):
  File "test.py", line 257, in <module>
    main(args, vis)
  File "test.py", line 65, in main
    test_loss = test(val_loader, model, args)
  File "test.py", line 203, in test
    pred.cpu().numpy(), lbl_map, cur_img, img_prefix
  File "/home/he/projects/videowalk/code/utils/test_utils.py", line 94, in dump_predictions
    pred_lbl = np.array(lbl_set, dtype=np.int32)[pred_lbl]
IndexError: index 206 is out of bounds for axis 0 with size 3
```

#### start from breakdance

```
computing affinity
173.68195056915283 affinity forward, max mem 1140.310546875
Traceback (most recent call last):
  File "test.py", line 257, in <module>
    main(args, vis)
  File "test.py", line 65, in main
    test_loss = test(val_loader, model, args)
  File "test.py", line 203, in test
    pred.cpu().numpy(), lbl_map, cur_img, img_prefix
  File "/home/he/projects/videowalk/code/utils/test_utils.py", line 94, in dump_predictions
    pred_lbl = np.array(lbl_set, dtype=np.int32)[pred_lbl]
IndexError: index 32 is out of bounds for axis 0 with size 2
> /home/he/projects/videowalk/code/utils/test_utils.py(94)dump_predictions()
-> pred_lbl = np.array(lbl_set, dtype=np.int32)[pred_lbl]
(Pdb)
```

## Post-Processing

```shell
# python eval/convert_davis.py --in_folder /save/path/ --out_folder /converted/path --dataset /davis/path/

# python /path/to/davis2017-evaluation/evaluation_method.py \
# --task semi-supervised   --results_path /converted/path --set val \
# --davis_path /path/to/davis/
```
