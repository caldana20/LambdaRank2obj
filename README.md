
LambdaRank with two objective function
=======================================

Installation
----------------
git clone https://github.com/caldana20/LightGBM.git -b lambdarank2obj

compile and install following https://lightgbm.readthedocs.io/en/latest/Installation-Guide.html:

```
git clone --recursive https://github.com/microsoft/LightGBM
cd LightGBM
mkdir build
cd build
cmake ..
make -j4
```


Usage
----------------
generate data by running gen_data.ipynb notebook

test_ltr2obj.ipynb test with extended MSLR-WEB10K dataset

```

    train_data = lightgbm.Dataset("./train_data")
    valid_data = lightgbm.Dataset("./valid_data")

    param = {
        'boosting_type':'gbdt',
        "objective": 'lambdarank2obj',
        'metric': 'ndcg',
        'ndcg_eval_at': [1, 3, 5, 10],
        'max_depth':10,
        'random_state':42,
        'lambdarank_norm':True,
        'lambdarank_truncation_level_obj2':30,
        'weight_obj2':0.3,
        'label_column':'label',
        'label2_column':'label2',
        'group_column':'name:query_id',
        'header': 'true'
    }
    
    bst = lightgbm.train(
        param, 
        train_data, 
        valid_sets=[valid_data],\
        verbose_eval=10)
```


Reference Papers
----------------

Svore, Krysta M., et al. “Learning to Rank with Multiple Objective Functions.” Proceedings of the 20th International Conference on World Wide Web - WWW ’11, ACM Press, 2011, p. 367. DOI.org (Crossref), https://doi.org/10.1145/1963405.1963459.



License
-------

This project is licensed under the terms of the MIT license. See [LICENSE](https://github.com/microsoft/LightGBM/blob/master/LICENSE) for additional details.
