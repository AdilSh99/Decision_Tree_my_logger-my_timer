# Decision-Tree

## Binder Badge to start the Binder environment:
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/GharbiRaouf/Decision_Tree_my_logger-my_timer/master)

## How to perform the exercise?
Click on the Launch Binder button, then a Binder window will open. A docker container with all necessary images will be created automatically. After a successful creation, a Jupyter window will be opened. Open Decision_Trees_Projekt.ipynb and then click on Run All at the top of Cell.

## Expected results ?
For this project we will use publicly available data from LendingClub.com. We will use data from 2007 to 2010 before the company went public. Using the data, we will try to predict whether a borrower has repaid the money or not. We have attached the data as CSV in the share price documentation.

1. Read data.
2. Explorative data analysis of data.
3. Generate some visualizations for a general overview.
4. Prepare data for a random forest classification model.
5. Training a decision tree model
6. Evaluation of data

## Timer & logger

In this section we will be documenting how we can log and get the execution time for certain functions.

As start we need to setup the necessary wrappers timer and logger as follow

```python
# Decorators
from functools import wraps

def my_logger(orig_func):
    import logging
    logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)

    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        logging.info(
            'Ran with args: {}, and kwargs: {}'.format(args, kwargs))
        return orig_func(*args, **kwargs)

    return wrapper


def my_timer(orig_func):
    import time

    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = orig_func(*args, **kwargs)
        t2 = time.time() - t1
        print('{} ran in: {} sec'.format(orig_func.__name__, t2))
        return result

    return wrapper
```

Next thing is to use these wrappers as follow:

```python
@my_logger 
@my_timer 
def dtreeFit ():
    return dtree.fit(X_train,y_train)
dtreeFit()
```

And as you can see these are the output after execution:
- Logger
![Screenshot](logger.PNG)

- Timer
![Screenshot](timer.PNG)


## Unit Tests

The first unit test case is reading its test data set from test_data.txt file.
The user is now able to change the data set for this test through one of the following methods:
```
Override the data set with new one in test_data.txt
Run unit tests
```
or
```
Remove test_data.txt 
Rename test_data2.txt to test_data.text
Run unit tests
```
