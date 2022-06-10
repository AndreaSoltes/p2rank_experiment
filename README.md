# p2rank_experiment
Model training and evaluation on Holo4k dataset splits

### Build used for training and evaluation:

https://github.com/rdk/p2rank/tree/836cb0189db3d6253372d60b896d7fa4b828b1bd

Memory in `local-env.sh` set to `"-Xmx128G"`

### Datasets:

Training on datasets:   
* `holo4k_train-fpocket.ds`
* `holo4k_val-fpocket.ds`

Evaluation on dataset: 
* `holo4k_test-fpocket.ds`

[Download Datasets](https://github.com/AndreaSoltes/p2rank_experiment/files/8843876/holo4k.dataset.splits.zip)

### Configurations:

Train and evaluation without conservation: `config/train-deafult.groovy`

Train and evaluation with conservation: `config/train-conservation.groovy`

[Download Configuration files](https://github.com/AndreaSoltes/p2rank_experiment/files/8879784/configurations.zip)

### Training prediction P2Rank model without conservation information

~~~bash
./prank.sh traineval -t ../p2rank-datasets/holo4k_train-fpocket.ds -e ../p2rank-datasets/holo4k_val-fpocket.ds -config config/train-default.groovy -rf_depth 12 -visualizations 0 -rf_threads 10 -rf_trees 100 -delete_models 0 -loop 1 -seed 42
~~~

### Evaluation of P2Rank model without conservation information

~~~bash
./prank.sh eval-predict -config config/train-default.groovy ../p2rank-datasets/holo4k_test-fpocket.ds -threads 4 -label pure -model ../p2rank-results/2.5-dev.3/traineval_holo4k_train-fpocket_holo4k_val-fpocket/runs/seed.42/FasterForest.model
~~~

### Results

`MCC=0.4794`

[Further Details](https://github.com/AndreaSoltes/p2rank_experiment/files/8879837/results_without_conservation.zip)

### Training prediction P2Rank model with conservation information

~~~bash
./prank.sh traineval -t ../p2rank-datasets/holo4k_train-fpocket.ds -e ../p2rank-datasets/holo4k_val-fpocket.ds -config config/train-conservation.groovy -rf_depth 12 -visualizations 0 -rf_threads 10 -rf_trees 100 -delete_models 0 -loop 1 -seed 42 -label conservation -conservation_dirs holo4k/conservation/e5i1/scores/
~~~

### Evaluation of P2Rank model with conservation information

~~~bash
./prank.sh eval-predict ../p2rank-datasets/holo4k_test-fpocket.ds -threads 4 -label conservation -model ../p2rank-results/2.5-dev.3/traineval_holo4k_train-fpocket_holo4k_val-fpocket_conservation/runs/seed.42/FasterForest.model -config config/train-conservation.groovy -conservation_dirs holo4k/conservation/e5i1/scores/
~~~

### Results

`MCC=0.5102`

[Further Details](https://github.com/AndreaSoltes/p2rank_experiment/files/8879836/results_with_conservation.zip)
