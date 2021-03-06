# Deep_Mortgage_Risk

This repository contains implementations of a five-layer neural network for predicting mortgage risk. Please read the paper [PDF](https://stanford.app.box.com/s/0iqyz2zt82uvqjb5cn8tskxxe7m0i0zo) for details. 

### Requirements
  * Python v3.5
  * TensorFlow v1.2+
  * Vtk v5.0+ (required for Mayavi)
  * Mayavi v4.5.0
  
For MacOSX, first install VTK with Homebrew, then install Mayavi with pip. 
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install
$ brew install vtk
$ mkdir -p /Users/[user]/Library/Python/2.7/lib/python/site-packages
$ echo 'import site; site.addsitedir("/usr/local/lib/python2.7/site-packages")' >> /Users/[user]/Library/Python/2.7/lib/python/site-packages/homebrew.pth
$ brew install wxpython
$ sudo pip install mayavi
```
For Linux, first install VTK, then install Mayavi. 
```
$ sudo apt-get install python-vtk
$ sudo pip install mayavi
```
For more 3D visualization, please refer to [LINK](http://www.sethanil.com/python-for-reseach/5). 

### Train, Validation & Test
- Logistic Regression
```
$ python3 run_logistic.py --mode=train --logdir=model/logistic --num_epochs=2
$ python3 run_logistic.py --mode=test --logdir=model/logistic
```
The table below reports test loss for the best model (on validation set): 

| Epoch | Train Loss | Validation Loss | Test Loss |
|:-----:|:----------:|:---------------:|:---------:|
| 1     | 0.1821     | 0.2111          | 0.1836    |

- Neural Network
```
$ python3 run.py --mode=train --logdir=model/neural --num_epochs=10
$ python3 run.py --mode=test --logdir=model/neural
```
The table below reports test loss for the best model (on validation set):

| Epoch | Train Loss | Validation Loss | Test Loss |
|:-----:|:----------:|:---------------:|:---------:|
| 9     | 0.1642     | 0.1930          | 0.1666    |

### Sensitivity Analysis
- Logistic Regression
```
$ python3 run_logistic.py --mode=sens_anlys --logdir=model/logistic
```
- Neural Network
```
$ python3 run.py --mode=sens_anlys --logdir=model/neural
$ python3 run.py --mode=sens_anlys_pair --logdir=model/neural --sample_size=1
$ python3 run.py --mode=sens_anlys_trio --logdir=model/neural --sample_size=1
```
Analysis results can be found in the folder "sens_anlys_output". 

### Analysis
```
$ python3 run_anlys.py --logdir=model/neural --task=1d_nonlinear --plot_out=plot # 1d Nonlinear 3D Plot
$ python3 run_anlys.py --logdir=model/neural --task=2d_nonlinear --plot_out=plot # 2d Nonlinear 3D Plot
$ python3 run_anlys.py --logdir=model/neural --task=2d_contour --plot_out=plot # 2d Nonlinear Contour Plot
$ python run_anlys.py --logdir=model/neural --task=3d_contour --plot_out=plot # 3d Nonlinear Contour Plot
$ python3 run_anlys.py --logdir=model/neural --task=3d_contour_slice --plot_out=plot # 3d Nonlinear Contour Slices
```
