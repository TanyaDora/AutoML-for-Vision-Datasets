# AutoML (Vision Data)

## Installation

To install the repository, first create an environment of your choice and activate it. 

For example, using `venv`:

You can change the python version here to the version you prefer.

**Virtual Environment**

```bash
python3 -m venv automl-vision-env
source automl-vision-env/bin/activate
```

**Conda Environment**

Can also use `conda`, left to individual preference.

```bash
conda create -n automl-vision-env python=3.11
conda activate automl-vision-env
```

Then install the repository by running the following command:

```bash
pip install -e .
```

You can test that the installation was successful by running the following command:

```bash
python -c "import automl"
```

We make no restrictions on the python library or version you use, but we recommend using python 3.8 or higher.

## Code

We provide the following:

* `run.py`: A script that trains an _AutoML-System_ on the training split `dataset_train` of a given dataset and then
  generates predictions for the test split `dataset_test`, saving those predictions to a file. For the training
  datasets, the test splits will contain the ground truth labels, but for the test dataset which we provide later the
  labels of the test split will not be available. You will be expected to generate these labels yourself and submit
  them to us through GitHub classrooms.

* `src/automl`: This is a python package that will be installed above and contain your source code for whatever
  system you would like to build. We have provided a dummy `AutoML` class to serve as an example.

**You are completely free to modify, install new libraries, make changes and in general do whatever you want with the
code.** The only requirement for the exam will be that you can generate predictions for the test splits of our datasets
in a `.npy` file that we can then use to give you a test score through GitHub classrooms.


## Data

We selected three different vision datasets which you can use to develop your AutoML system and we will provide you with
a test dataset to evaluate your system at a later point in time. The datasets can be automatically downloaded by the
respective dataset classes in `./src/automl/datasets.py`. The datasets are: _fashion_, _flowers_, and _emotions_.

If there are any problems downloading the datasets, you can download them manually
from https://ml.informatik.uni-freiburg.de/research-artifacts/automl-exam-24-vision/ and place them in the `/data` folder
after unzipping them.

The downloaded datasets will have the following structure:
```bash
./data
├── fashion
│   ├── images_test
│   │   ├── 000001.jpg
│   │   ├── 000002.jpg
│   │   ├── 000003.jpg
│   │   ...
│   ├── images_train
│   │   ├── 000001.jpg
│   │   ├── 000002.jpg
│   │   ├── 000003.jpg
│   │   ...
│   ├── description.md
│   ├── fashion.tgz
│   ├── test.csv
│   └── train.csv
├── emotions
    ...
...
```
Feel free to explore the images and the `description.md` files to get a better understanding of the datasets.
The following table will provide you an overview of their characteristics and also a reference value for the 
accuracy that a naive AutoML system could achieve on these datasets:

| Dataset name | # Classes | # Train samples | # Test samples | # Channels | Resolution | Reference Accuracy |
|--------------|-----------|-----------------|----------------|------------|------------|--------------------|
| fashion      | 10        | 60,000          | 10,000         | 1          | 28x28      | 0.88               |
| flowers      | 102*      | 5732            | 2,457          | 3          | 512x512    | 0.55               |
| emotions     | 7         | 28709           | 7,178          | 1          | 48x48      | 0.40               |
| **skin_cancer**  |**7\***       | **7,010**          | **3,005**          | **3**          | **450x450**    | **0.71**               |

*classes are imbalanced

We will add the test dataset later by pushing its class definition to the `datasets.py` file. 
The test dataset will be in the same
format as the training datasets, but `test.csv` will only contain nan's for labels.

**Update**: We now provide the `skin_cancer` test dataset. 


## Running an initial test

This will download the _fashion_ dataset into `./data`, train a dummy AutoML system and generate predictions for the test
split:

```bash 
python run.py --dataset fashion --seed 42 --output-path preds-42-fashion.npy
```

## Running auto evaluation on test dataset

Only activates on the `test` branch:
```bash
git checkout -b test  # to create the branch
# or
# if branch exists
git checkout test
git merge <name-of-branch-where-current-code-to-test-exists>
# ensure that your latest `predictions.npy` exists
git push origin test  # depending on MERGE-CONFLICTS might need to resolve and add files
# wait for some time (few minutes) or monitor the web UI of Github to see Actions passing
git pull
# test scores will be downloaded under `./exam_dataset/test_out/`
```

* To initialize auto-evaluation for the test data, create a `test` branch. 
* After publishing it, the evaluation script will automatically trigger.
* After creating the `test` branch, you may also run the evaluation script on any other branch manually.
  * To do that, navigate to the `Actions` tab at the GitHub remote repository and proceed by pressing the `Run workflow` button.
  * Triggering the workflow by pushing to the `test` branch is highly recommended for your own logging purposes (use the commit message).
* For the evaluation to run correctly, make sure the `predictions.npy` is at the right location.
* The results are also pushed to your repo (don't forget to `git pull`)
* If no test predictions generated, check the errors in the Github action (red cross inline with your last commit on the test branch)

```bash
./data
├── skin_cancer
└── auto_evaluation
│   └── predictions.npy
│   └── test_out
│   │   ├── test_evaluation_output_2024-MM-DD_HH-mm
.   .   .
```
