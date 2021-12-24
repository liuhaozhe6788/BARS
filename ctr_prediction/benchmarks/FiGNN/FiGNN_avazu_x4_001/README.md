## FiGNN_Avazu_x4_001

A notebook to benchmark FiGNN on Avazu_x4_001 dataset.

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
In this setting, we preprocess the data split by removing the id field that is useless for CTR prediction. In addition, we transform the timestamp field into three fields: hour, weekday, and is_weekend. For all categorical fields, we filter infrequent features by setting the threshold min_category_count=2 (performs well) and replace them with a default <OOV> token. Note that we do not follow the exact preprocessing steps in AutoInt, because the authors neither remove the useless id field nor specially preprocess the timestamp field.

To make a fair comparison, we fix embedding_dim=16 as with AutoInt.


### Code
1. Install FuxiCTR
  
    Install FuxiCTR via `pip install fuxictr==1.0` to get all dependencies ready. Then download [the FuxiCTR repository](https://github.com/huawei-noah/benchmark/archive/53e314461c19dbc7f462b42bf0f0bfae020dc398.zip) to your local path.

2. Downalod the dataset and run [the preprocessing script](https://github.com/xue-pai/Open-CTR-Benchmark/blob/master/datasets/Avazu/Avazu_x4/split_avazu_x4.py) for data splitting. 

3. Download the hyper-parameter configuration file: [FiGNN_avazu_x4_tuner_config_03.yaml](./FiGNN_avazu_x4_tuner_config_03.yaml)

4. Run the following script to reproduce the result. 
  + --config: The config file that defines the tuning space
  + --tag: Specify which expid to run (each expid corresponds to a specific setting of hyper-parameters in the tunner space)
  + --gpu: The available gpus for parameters tuning.

  ```bash
  cd FuxiCTR/benchmarks
  python run_param_tuner.py --config YOUR_PATH/FiGNN_avazu_x4_tuner_config_03.yaml --tag 002 --gpu 0
  ```


### Results
```python
[Metrics] logloss: 0.373630 - AUC: 0.791460
```


### Logs
```python
2020-06-14 14:51:44,937 P591 INFO {
    "batch_size": "10000",
    "data_format": "h5",
    "data_root": "../data/Avazu/",
    "dataset_id": "avazu_x4_3bbbc4c9",
    "debug": "False",
    "embedding_dim": "16",
    "embedding_dropout": "0",
    "embedding_regularizer": "1e-06",
    "epochs": "100",
    "every_x_epochs": "1",
    "gnn_layers": "9",
    "gpu": "1",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['logloss', 'AUC']",
    "model": "FiGNN",
    "model_id": "FiGNN_avazu_x4_3bbbc4c9_002_236c17be",
    "model_root": "./Avazu/FiGNN_avazu/min2/",
    "monitor": "{'AUC': 1, 'logloss': -1}",
    "monitor_mode": "max",
    "net_regularizer": "0",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "reuse_graph_layer": "False",
    "save_best_only": "True",
    "seed": "2019",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Avazu/avazu_x4_3bbbc4c9/test.h5",
    "train_data": "../data/Avazu/avazu_x4_3bbbc4c9/train.h5",
    "use_gru": "False",
    "use_hdf5": "True",
    "use_residual": "True",
    "valid_data": "../data/Avazu/avazu_x4_3bbbc4c9/valid.h5",
    "verbose": "0",
    "version": "pytorch",
    "workers": "3"
}
2020-06-14 14:51:44,940 P591 INFO Set up feature encoder...
2020-06-14 14:51:44,940 P591 INFO Load feature_map from json: ../data/Avazu/avazu_x4_3bbbc4c9/feature_map.json
2020-06-14 14:51:44,940 P591 INFO Loading data...
2020-06-14 14:51:44,952 P591 INFO Loading data from h5: ../data/Avazu/avazu_x4_3bbbc4c9/train.h5
2020-06-14 14:51:47,781 P591 INFO Loading data from h5: ../data/Avazu/avazu_x4_3bbbc4c9/valid.h5
2020-06-14 14:51:48,991 P591 INFO Train samples: total/32343172, pos/5492052, neg/26851120, ratio/16.98%
2020-06-14 14:51:49,112 P591 INFO Validation samples: total/4042897, pos/686507, neg/3356390, ratio/16.98%
2020-06-14 14:51:49,112 P591 INFO Loading train data done.
2020-06-14 14:51:58,854 P591 INFO Start training: 3235 batches/epoch
2020-06-14 14:51:58,854 P591 INFO ************ Epoch=1 start ************
2020-06-14 15:06:58,880 P591 INFO [Metrics] logloss: 0.375680 - AUC: 0.787305
2020-06-14 15:06:58,881 P591 INFO Save best model: monitor(max): 0.411625
2020-06-14 15:06:59,607 P591 INFO --- 3235/3235 batches finished ---
2020-06-14 15:06:59,664 P591 INFO Train loss: 0.390001
2020-06-14 15:06:59,665 P591 INFO ************ Epoch=1 end ************
2020-06-14 15:21:57,976 P591 INFO [Metrics] logloss: 0.373721 - AUC: 0.791325
2020-06-14 15:21:57,980 P591 INFO Save best model: monitor(max): 0.417604
2020-06-14 15:21:58,509 P591 INFO --- 3235/3235 batches finished ---
2020-06-14 15:21:58,568 P591 INFO Train loss: 0.372816
2020-06-14 15:21:58,568 P591 INFO ************ Epoch=2 end ************
2020-06-14 15:36:55,798 P591 INFO [Metrics] logloss: 0.375492 - AUC: 0.790293
2020-06-14 15:36:55,802 P591 INFO Monitor(max) STOP: 0.414801 !
2020-06-14 15:36:55,802 P591 INFO Reduce learning rate on plateau: 0.000100
2020-06-14 15:36:55,802 P591 INFO --- 3235/3235 batches finished ---
2020-06-14 15:36:55,854 P591 INFO Train loss: 0.358890
2020-06-14 15:36:55,854 P591 INFO ************ Epoch=3 end ************
2020-06-14 15:51:56,158 P591 INFO [Metrics] logloss: 0.403222 - AUC: 0.777821
2020-06-14 15:51:56,162 P591 INFO Monitor(max) STOP: 0.374599 !
2020-06-14 15:51:56,162 P591 INFO Reduce learning rate on plateau: 0.000010
2020-06-14 15:51:56,162 P591 INFO Early stopping at epoch=4
2020-06-14 15:51:56,162 P591 INFO --- 3235/3235 batches finished ---
2020-06-14 15:51:56,216 P591 INFO Train loss: 0.314782
2020-06-14 15:51:56,216 P591 INFO Training finished.
2020-06-14 15:51:56,216 P591 INFO Load best model: /cache/xxx/FuxiCTR/benchmarks/Avazu/FiGNN_avazu/min2/avazu_x4_3bbbc4c9/FiGNN_avazu_x4_3bbbc4c9_002_236c17be_model.ckpt
2020-06-14 15:51:56,700 P591 INFO ****** Train/validation evaluation ******
2020-06-14 15:55:11,710 P591 INFO [Metrics] logloss: 0.327311 - AUC: 0.855957
2020-06-14 15:55:34,878 P591 INFO [Metrics] logloss: 0.373721 - AUC: 0.791325
2020-06-14 15:55:34,961 P591 INFO ******** Test evaluation ********
2020-06-14 15:55:34,962 P591 INFO Loading data...
2020-06-14 15:55:34,962 P591 INFO Loading data from h5: ../data/Avazu/avazu_x4_3bbbc4c9/test.h5
2020-06-14 15:55:35,584 P591 INFO Test samples: total/4042898, pos/686507, neg/3356391, ratio/16.98%
2020-06-14 15:55:35,584 P591 INFO Loading test data done.
2020-06-14 15:56:00,588 P591 INFO [Metrics] logloss: 0.373630 - AUC: 0.791460


```