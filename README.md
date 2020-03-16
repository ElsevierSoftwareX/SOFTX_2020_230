# pspso

pspso is a python library for selecting machine learning algorithms parameters.
The first version supports two single algorithms: Multi-Layer Perceptron (MLP) and Support Vector Machine (SVM).
It supports two ensembles: Extreme Gradient Boosting (XGBoost) and Gradient Boosting Decision Trees (GBDT).

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install pspso.

```bash
pip install pspso
```

## Usage

### MLP Example
pspso is used to select the machine learning algorithms parameters. It is assumed that the user
has already processed and prepared the training and validation datasets. Below is an example for using the 
pso to select the parameters of the MLP. It should be noticed that pspso handles the MLP random weights intialization issue
that may cause losing the best solution in consecutive iterations.
```python
from pspso import pspso
params = {"optimizer":['adam','nadam','sgd','adadelta'],
    "learning_rate":  [0.01,0.2,2],
    "hiddenactivation": ['sigmoid','tanh','relu'],
    "activation": ['sigmoid','tanh','relu']}
task='binary classification'
score='auc'
number_of_particles=4
number_of_iterations=5
p=pspso('mlp',params,task,score)
p.fitpspso(X_train,Y_train,X_val,Y_val,number_of_particles=number_of_particles,
               number_of_iterations=number_of_iterations)
p.printresults()
```

In this example, four parameters were examined: optimizer, learning_rate, hiddenactivation, and activation.
The number of neurons in the hidden layer was kept as default.

### Details

The user is given the chance to handle some of the default parameters such as the number of epochs. 
The user can modify this by changing a pspso class intance. For e.g., if you need to change the number of epochs from 50 
to 10 for an MLP training:
```python
from pspso import pspso
task='binary classification'
score='auc'
p=pspso.pspso('mlp',params,task,score)
p.defaultparams['epochs']=10

```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)