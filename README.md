### Testing the model:

1. ##### Install an Anaconda distribution with Python 3

   The following has been tested using a full Anaconda distribution, but [Miniconda](https://conda.io/en/latest/miniconda.html) is probably sufficient and will take less time to install.

2. ##### Clone or download the repository

    `git clone https://github.com/g-simmons/dairyML.git` 

   or download using the green "clone or download" button on the right

3. ##### Set up an environment with the necessary packages

   `cd DairyML`

   `conda env create -f environment_test_min.yml`

   `conda activate dmltest`

   (Note that this will only install the minimum requirements for testing the most recent model. The full development environment can be installed with `conda env create -f environment_full.yml`)

4. ##### Place your test data in `data/` directory

   Make sure that the test data columns match the columns of `data/training_for_GS_122118.csv`

5. ##### Run the test script

   Test script usage is: python test.py <model_path> <data_path>

   For example, from the main directory:

   `python src/test.py models/xgb_combined.model data/<test_data_filename>.csv`

   Example output:

   ```
   (dmltest) C:\Users\Gabriel\DairyML>python src/test.py models/xgb_combined.model
   data/training_for_GS_122118.csv
   Loading modules...
   Loading model at models/xgb_combined.model
   Loading data at data/training_for_GS_122118.csv
   Scaling input features...
   Removing outliers...
   Outliers removed: 5
   Testing the model... (10-fold CV, repeated 5x)
   
   Results:
   r2: 0.81
   SRC: 0.9
   PCC: 0.91
   MI: 3.02
   MAE: 0.44
   
   Results saved to ../reports/test_results_2019-02-19-11-08-34.csv
   ```

6. ##### Results are stored to csv in reports/



### Using the model in your own code

This starter code has not been tested, but this is what using the model would look like. It is stored as a binary object using pickle, and can be loaded using pickle.load.

See the test script for more info. If you simply want to change the cross-validation parameters, these can be adjusted by changing

```
N_SPLITS = 10
N_REPEATS = 5
```

to new values in` test.py` 



Ex code

```python
import pickle as pkl
from xgboost import XGBRegressor, XGBClassifier
from dairyml import XGBCombined
  
model_path = <specify model path>

with open(model_path, "rb" ) as f:
	model = pkl.load(f)

#do stuff with the model, e.g.
#X = features
#Y = target variable
model.fit(X,Y)
predictions = model.predict(X_new)

```
