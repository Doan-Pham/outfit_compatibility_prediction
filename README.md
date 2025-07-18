## Introduction
- An OutfitTransformer AI model for Outfit Compatibility Prediction
- Reserach paper for reference: [OutfitTransformer: Outfit Representations for Fashion Recommendation](https://arxiv.org/abs/2204.04812) by Rohan Sarkar, Navaneeth Bodla, Mariya I. Vasileva, Yen-Liang Lin, Anurag Beniwal, Alan and và Gerard Medioni
- Tech stack: Python, Numpy, Pytorch, Streamlit
## Setup
1. Clone this repository with [Git](https://git-scm.com)
```bash
git clone https://github.com/Doan-Pham/outfit_compatibility_prediction.git
```
2. Download and extract this file [data.zip (2.3GB)](https://drive.google.com/file/d/1696cpHFamwTH9ViyUYlPHCvL0X52Ww16/view?usp=sharing) to the same folder as the repository
3. Download miniconda3 (A package manager và virtual environment for Python) from [miniconda3](https://docs.conda.io/projects/miniconda/en/latest/)
4. After installation, open Anaconda Prompt (miniconda3)
![Untitled](https://github.com/Doan-Pham/outfit_recommendation/assets/85011400/c0d78c1b-19a8-44bd-ba78-327e13379994)

5. Run the following command to create Anaconda virtual environment with the necessary dependencies.
```bash
conda create -n outfit_recommendation --file requirements.txt
```

## How to run
1. Open Anaconda Prompt and change directory to the repository's directory:
```bash
cd path/to/your/repo/outfit_recommendation
```
2. Activate the virtual environment created in setup step
```bash
conda activate outfit_recommendation
```

3. Run the following command to start training model:
```bash
python main.py
```
By default, the training will not be carried out on the whole dataset. Instead, the model is only trained on a data subset for illustration purpose. To train the model with the whole subset, run the following command:
```bash
python main.py --run_real 1
```
The training result of each epoch will be saved to `checkpoint/disjoint`. Inside, `checkpoint_0.pt`, `checkpoint_1.pt` files are the training results of each epoch, while  `best_state.pt` is the best result of all epochs

You can run the following command to know all possible arguments with `python main.py`:
```bash
python main.py --help
```
Result after running `python main.py --help`
```bash
usage: main.py [-h] [--datazip DATAZIP] [--run_real RUN_REAL]
               [--log_level LOG_LEVEL] [--datadir DATADIR]
               [--checkpoint_dir CHECKPOINT_DIR] [--batch_size BATCH_SIZE]
               [--polyvore_split POLYVORE_SPLIT] [--epochs EPOCHS]

options:
  -h, --help            show this help message and exit
  --datazip DATAZIP     Path to input data zip file
  --run_real RUN_REAL   0 = train with few data to see model run; 1 = train with    
                        whole dataset. Default is 0
  --log_level LOG_LEVEL
                        0 = Print >= warnings, 1 = print >= info, 2 = print all     
  --datadir DATADIR     Path to data directory
  --checkpoint_dir CHECKPOINT_DIR
                        Path to the directory to save checkpoints
  --batch_size BATCH_SIZE
                        Batch size in training, default is 50
  --polyvore_split POLYVORE_SPLIT
                        The split of the polyvore data (disjoint or nondisjoint)    
  --epochs EPOCHS       Number of epochs to train for (default: 10)
```
For example: If you want to run `python main.py` to train model in 15 epochs, with batch size being 30 items. Also, you want to get training data from `data.zip` file instead of the extracted folder, and train on the whole dataset. You can run the folliwing command:
```bash
python main.py --epochs 15 --batch_size 30 --datazip data.zip --run_real 1
```
**Note**: Training with a large amount of data on your local machien can causes IDE crash due to out-of-memory error. You can reduce bacth_size or leave --run_real as 0 (Or use cloud solutions for training model).
4. After training the model for at least 1 epoch (Or you can download [a pre-trained model here(240 MB)](https://drive.google.com/file/d/1GnA3LGX_bTvWn08k0SPaEzNaxHSSljMn/view?usp=sharing) and extract to the repository directory), You can run the following command to open the demo app. This app will apply the parameters from `best_state.pt` to give inferences:
```bash
streamlit run demo_app.py
```

## Authors:
- Pham Truong Hai Doan (Leader) - Build and train model
- Mai Pham Quoc Hung - Build demo app


