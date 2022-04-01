# yujie_eval_notes

- env

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

- res

```shell
...
computing resized lbl for //home/he/data/davis/Annotations/480p/blackswan/00048_size60x107.npy
computing onehot lbl for //home/he/data/davis/Annotations/480p/blackswan/00049_onehot.npy
computing resized lbl for //home/he/data/davis/Annotations/480p/blackswan/00049_size60x107.npy
******* Vid 1 (70 frames) *******
computed features 1.143826961517334
Killed
```

## Post-Processing:

```shell
# python eval/convert_davis.py --in_folder /save/path/ --out_folder /converted/path --dataset /davis/path/

# python /path/to/davis2017-evaluation/evaluation_method.py \
# --task semi-supervised   --results_path /converted/path --set val \
# --davis_path /path/to/davis/
```
