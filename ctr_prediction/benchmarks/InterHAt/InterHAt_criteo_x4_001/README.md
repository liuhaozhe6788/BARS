## InterHAt_Criteo_x4_001 

A notebook to benchmark InterHAt on Criteo_x4_001 dataset.

Author: [XUEPAI Team](https://github.com/xue-pai)


### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  RAM: 500G+
  ```
+ Software

  ```python
  python: 3.6.5
  pandas: 1.0.0
  numpy: 1.18.1
  ```

### Dataset
In this setting, we follow the winner's solution of the Criteo challenge to discretize each integer value x to ⌊log2
(x)⌋, if x > 2; and x = 1 otherwise. For all categorical fields, we replace infrequent features with a default ``<OOV>`` token by setting the threshold min_category_count=10. Note that we do not follow the exact preprocessing steps in AutoInt, because this preprocessing performs much better. 

To make a fair comparison, we fix **embedding_dim=16** as with AutoInt.


### Code
1. Install FuxiCTR
  
    Install FuxiCTR via `pip install fuxictr==1.0` to get all dependencies ready. Then download [the FuxiCTR repository](https://github.com/huawei-noah/benchmark/archive/53e314461c19dbc7f462b42bf0f0bfae020dc398.zip) to your local path.

2. Downalod the dataset and run [the preprocessing script](https://github.com/xue-pai/Open-CTR-Benchmark/blob/master/datasets/Criteo/Criteo_x4/split_criteo_x4.py) for data splitting. 

3. Download the hyper-parameter configuration file: [InterHAt_criteo_x4_tuner_config_02.yaml](./InterHAt_criteo_x4_tuner_config_02.yaml)

4. Run the following script to reproduce the result. 
  + --config: The config file that defines the tuning space
  + --tag: Specify which expid to run (each expid corresponds to a specific setting of hyper-parameters in the tunner space)
  + --gpu: The available gpus for parameters tuning.

  ```bash
  cd FuxiCTR/benchmarks
  python run_param_tuner.py --config YOUR_PATH/InterHAt_criteo_x4_tuner_config_02.yaml --tag 006 --gpu 0
  ```



### Results
```python
[Metrics] logloss: 0.441355 - AUC: 0.810419
```


### Logs
```python
2020-07-02 18:16:23,093 P2291 INFO {
    "attention_dim": "16",
    "batch_norm": "False",
    "batch_size": "10000",
    "data_format": "h5",
    "data_root": "../data/Criteo/",
    "dataset_id": "criteo_x4_5c863b0f",
    "debug": "False",
    "embedding_dim": "16",
    "embedding_regularizer": "1e-05",
    "epochs": "100",
    "every_x_epochs": "1",
    "gpu": "0",
    "hidden_activations": "relu",
    "hidden_dim": "500",
    "hidden_units": "[1000, 1000]",
    "layer_norm": "True",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['logloss', 'AUC']",
    "model": "InterHAt",
    "model_id": "InterHAt_criteo_x4_5c863b0f_006_70750e09",
    "model_root": "./Criteo/InterHAt_criteo/min10/",
    "monitor": "{'AUC': 1, 'logloss': -1}",
    "monitor_mode": "max",
    "net_dropout": "0",
    "net_regularizer": "0",
    "num_heads": "2",
    "optimizer": "adam",
    "order": "2",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2019",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Criteo/criteo_x4_5c863b0f/test.h5",
    "train_data": "../data/Criteo/criteo_x4_5c863b0f/train.h5",
    "use_hdf5": "True",
    "use_residual": "False",
    "valid_data": "../data/Criteo/criteo_x4_5c863b0f/valid.h5",
    "verbose": "0",
    "version": "pytorch",
    "workers": "3"
}
2020-07-02 18:16:23,093 P2291 INFO Set up feature encoder...
2020-07-02 18:16:23,094 P2291 INFO Load feature_map from json: ../data/Criteo/criteo_x4_5c863b0f/feature_map.json
2020-07-02 18:16:23,094 P2291 INFO Loading data...
2020-07-02 18:16:23,095 P2291 INFO Loading data from h5: ../data/Criteo/criteo_x4_5c863b0f/train.h5
2020-07-02 18:16:28,309 P2291 INFO Loading data from h5: ../data/Criteo/criteo_x4_5c863b0f/valid.h5
2020-07-02 18:16:30,533 P2291 INFO Train samples: total/36672493, pos/9396350, neg/27276143, ratio/25.62%
2020-07-02 18:16:30,663 P2291 INFO Validation samples: total/4584062, pos/1174544, neg/3409518, ratio/25.62%
2020-07-02 18:16:30,663 P2291 INFO Loading train data done.
2020-07-02 18:16:35,578 P2291 INFO Start training: 3668 batches/epoch
2020-07-02 18:16:35,579 P2291 INFO ************ Epoch=1 start ************
2020-07-02 18:27:17,121 P2291 INFO [Metrics] logloss: 0.452976 - AUC: 0.797237
2020-07-02 18:27:17,123 P2291 INFO Save best model: monitor(max): 0.344261
2020-07-02 18:27:17,189 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 18:27:17,255 P2291 INFO Train loss: 0.465594
2020-07-02 18:27:17,256 P2291 INFO ************ Epoch=1 end ************
2020-07-02 18:37:56,494 P2291 INFO [Metrics] logloss: 0.450133 - AUC: 0.801286
2020-07-02 18:37:56,496 P2291 INFO Save best model: monitor(max): 0.351152
2020-07-02 18:37:56,581 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 18:37:56,691 P2291 INFO Train loss: 0.459640
2020-07-02 18:37:56,691 P2291 INFO ************ Epoch=2 end ************
2020-07-02 18:48:35,150 P2291 INFO [Metrics] logloss: 0.448979 - AUC: 0.802505
2020-07-02 18:48:35,152 P2291 INFO Save best model: monitor(max): 0.353527
2020-07-02 18:48:35,253 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 18:48:35,315 P2291 INFO Train loss: 0.457788
2020-07-02 18:48:35,315 P2291 INFO ************ Epoch=3 end ************
2020-07-02 18:59:11,753 P2291 INFO [Metrics] logloss: 0.448258 - AUC: 0.803106
2020-07-02 18:59:11,754 P2291 INFO Save best model: monitor(max): 0.354848
2020-07-02 18:59:11,839 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 18:59:11,901 P2291 INFO Train loss: 0.456947
2020-07-02 18:59:11,901 P2291 INFO ************ Epoch=4 end ************
2020-07-02 19:09:48,856 P2291 INFO [Metrics] logloss: 0.447542 - AUC: 0.803528
2020-07-02 19:09:48,858 P2291 INFO Save best model: monitor(max): 0.355986
2020-07-02 19:09:48,946 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 19:09:49,009 P2291 INFO Train loss: 0.456445
2020-07-02 19:09:49,009 P2291 INFO ************ Epoch=5 end ************
2020-07-02 19:20:20,350 P2291 INFO [Metrics] logloss: 0.447376 - AUC: 0.804157
2020-07-02 19:20:20,351 P2291 INFO Save best model: monitor(max): 0.356781
2020-07-02 19:20:20,436 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 19:20:20,523 P2291 INFO Train loss: 0.456083
2020-07-02 19:20:20,524 P2291 INFO ************ Epoch=6 end ************
2020-07-02 19:30:51,758 P2291 INFO [Metrics] logloss: 0.447191 - AUC: 0.804321
2020-07-02 19:30:51,759 P2291 INFO Save best model: monitor(max): 0.357130
2020-07-02 19:30:51,860 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 19:30:51,921 P2291 INFO Train loss: 0.455792
2020-07-02 19:30:51,921 P2291 INFO ************ Epoch=7 end ************
2020-07-02 19:41:21,732 P2291 INFO [Metrics] logloss: 0.447030 - AUC: 0.804668
2020-07-02 19:41:21,733 P2291 INFO Save best model: monitor(max): 0.357638
2020-07-02 19:41:21,820 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 19:41:21,881 P2291 INFO Train loss: 0.455588
2020-07-02 19:41:21,881 P2291 INFO ************ Epoch=8 end ************
2020-07-02 19:51:56,259 P2291 INFO [Metrics] logloss: 0.446510 - AUC: 0.804836
2020-07-02 19:51:56,261 P2291 INFO Save best model: monitor(max): 0.358326
2020-07-02 19:51:56,362 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 19:51:56,423 P2291 INFO Train loss: 0.455393
2020-07-02 19:51:56,423 P2291 INFO ************ Epoch=9 end ************
2020-07-02 20:02:27,492 P2291 INFO [Metrics] logloss: 0.446532 - AUC: 0.805302
2020-07-02 20:02:27,493 P2291 INFO Save best model: monitor(max): 0.358770
2020-07-02 20:02:27,576 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 20:02:27,658 P2291 INFO Train loss: 0.455227
2020-07-02 20:02:27,658 P2291 INFO ************ Epoch=10 end ************
2020-07-02 20:12:58,106 P2291 INFO [Metrics] logloss: 0.445965 - AUC: 0.805306
2020-07-02 20:12:58,107 P2291 INFO Save best model: monitor(max): 0.359341
2020-07-02 20:12:58,189 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 20:12:58,256 P2291 INFO Train loss: 0.455075
2020-07-02 20:12:58,256 P2291 INFO ************ Epoch=11 end ************
2020-07-02 20:23:36,219 P2291 INFO [Metrics] logloss: 0.445917 - AUC: 0.805492
2020-07-02 20:23:36,221 P2291 INFO Save best model: monitor(max): 0.359575
2020-07-02 20:23:36,335 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 20:23:36,394 P2291 INFO Train loss: 0.454916
2020-07-02 20:23:36,394 P2291 INFO ************ Epoch=12 end ************
2020-07-02 20:34:12,792 P2291 INFO [Metrics] logloss: 0.445498 - AUC: 0.805647
2020-07-02 20:34:12,793 P2291 INFO Save best model: monitor(max): 0.360148
2020-07-02 20:34:12,882 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 20:34:12,945 P2291 INFO Train loss: 0.454781
2020-07-02 20:34:12,945 P2291 INFO ************ Epoch=13 end ************
2020-07-02 20:44:49,383 P2291 INFO [Metrics] logloss: 0.445492 - AUC: 0.805812
2020-07-02 20:44:49,384 P2291 INFO Save best model: monitor(max): 0.360320
2020-07-02 20:44:49,467 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 20:44:49,532 P2291 INFO Train loss: 0.454669
2020-07-02 20:44:49,533 P2291 INFO ************ Epoch=14 end ************
2020-07-02 20:55:26,126 P2291 INFO [Metrics] logloss: 0.445413 - AUC: 0.805929
2020-07-02 20:55:26,127 P2291 INFO Save best model: monitor(max): 0.360516
2020-07-02 20:55:26,227 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 20:55:26,314 P2291 INFO Train loss: 0.454572
2020-07-02 20:55:26,314 P2291 INFO ************ Epoch=15 end ************
2020-07-02 21:06:02,289 P2291 INFO [Metrics] logloss: 0.445724 - AUC: 0.806034
2020-07-02 21:06:02,291 P2291 INFO Monitor(max) STOP: 0.360310 !
2020-07-02 21:06:02,291 P2291 INFO Reduce learning rate on plateau: 0.000100
2020-07-02 21:06:02,291 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 21:06:02,353 P2291 INFO Train loss: 0.454483
2020-07-02 21:06:02,353 P2291 INFO ************ Epoch=16 end ************
2020-07-02 21:16:39,369 P2291 INFO [Metrics] logloss: 0.441999 - AUC: 0.809565
2020-07-02 21:16:39,371 P2291 INFO Save best model: monitor(max): 0.367566
2020-07-02 21:16:39,478 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 21:16:39,545 P2291 INFO Train loss: 0.445291
2020-07-02 21:16:39,545 P2291 INFO ************ Epoch=17 end ************
2020-07-02 21:27:17,308 P2291 INFO [Metrics] logloss: 0.441632 - AUC: 0.810048
2020-07-02 21:27:17,310 P2291 INFO Save best model: monitor(max): 0.368416
2020-07-02 21:27:17,397 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 21:27:17,458 P2291 INFO Train loss: 0.441358
2020-07-02 21:27:17,458 P2291 INFO ************ Epoch=18 end ************
2020-07-02 21:37:52,788 P2291 INFO [Metrics] logloss: 0.441730 - AUC: 0.809964
2020-07-02 21:37:52,789 P2291 INFO Monitor(max) STOP: 0.368234 !
2020-07-02 21:37:52,789 P2291 INFO Reduce learning rate on plateau: 0.000010
2020-07-02 21:37:52,789 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 21:37:52,850 P2291 INFO Train loss: 0.439328
2020-07-02 21:37:52,851 P2291 INFO ************ Epoch=19 end ************
2020-07-02 21:48:30,640 P2291 INFO [Metrics] logloss: 0.442772 - AUC: 0.809289
2020-07-02 21:48:30,641 P2291 INFO Monitor(max) STOP: 0.366516 !
2020-07-02 21:48:30,641 P2291 INFO Reduce learning rate on plateau: 0.000001
2020-07-02 21:48:30,641 P2291 INFO Early stopping at epoch=20
2020-07-02 21:48:30,641 P2291 INFO --- 3668/3668 batches finished ---
2020-07-02 21:48:30,701 P2291 INFO Train loss: 0.434674
2020-07-02 21:48:30,702 P2291 INFO Training finished.
2020-07-02 21:48:30,702 P2291 INFO Load best model: /cache/xxx/FuxiCTR/benchmarks/Criteo/InterHAt_criteo/min10/criteo_x4_5c863b0f/InterHAt_criteo_x4_5c863b0f_006_70750e09_model.ckpt
2020-07-02 21:48:30,803 P2291 INFO ****** Train/validation evaluation ******
2020-07-02 21:52:27,871 P2291 INFO [Metrics] logloss: 0.431493 - AUC: 0.820987
2020-07-02 21:52:56,732 P2291 INFO [Metrics] logloss: 0.441632 - AUC: 0.810048
2020-07-02 21:52:56,819 P2291 INFO ******** Test evaluation ********
2020-07-02 21:52:56,819 P2291 INFO Loading data...
2020-07-02 21:52:56,819 P2291 INFO Loading data from h5: ../data/Criteo/criteo_x4_5c863b0f/test.h5
2020-07-02 21:52:57,487 P2291 INFO Test samples: total/4584062, pos/1174544, neg/3409518, ratio/25.62%
2020-07-02 21:52:57,487 P2291 INFO Loading test data done.
2020-07-02 21:53:26,086 P2291 INFO [Metrics] logloss: 0.441355 - AUC: 0.810419
```