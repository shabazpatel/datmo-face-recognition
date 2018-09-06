### Face Recognition

#### a. Introduction

This is a tutorial on face recognition to show case classifiers built using datmo, in order to track our work and make machine learning workflow reproducible and usable. We have built classifier for facial recognition, with very few images here. The accuracy from this tutorial can be improved with more training images. You can also increase the number of classes or faces. 

During this experimentation, we perform model engineering and will be using datmo to create versions of work by creating snapshot.

#### b. Installation
To use datmo, you can install it using pip install datmo after having the Docker as the prerequisites as in this [README](https://github.com/datmo/datmo)

```
$ pip install datmo
```

To run the experimentation.ipynb file, you can run it with datmo notebook command, it uses docker for environment management.

```bash
home:~/datmo-face-recognition$ datmo init
press enter to skip the default environment setup and run the jupyter notebook
home:~/datmo-face-recognition$ datmo notebook
```
#### c. Solution
After the installation, we run the experimentation.ipynb notebook and perform following steps,

* Visualizing the images
* Face detection
* Extracting facial encoding to train a classifier
* Using random forest classifier 
* Using KNN classifier

#### d. Creating versions or snapshots
During the process of model engineering, we will be using datmo to create versions of work by creating datmo snapshots. As you see below, we created two snapshots at the end of the notebook tutorial. More information about the flow can be found in the notebook file.

```bash
home:~/datmo-face-recognition$ datmo snapshot create -m "knn classifier"
Creating a new snapshot
Created snapshot with id: 7a3530f742
```

After running this, you should be able to view the created snapshot using the command, `snapshot ls`

```bash
home:~/datmo-face-recognition$ datmo snapshot ls
+-------------+-----------+--------------------+---------------+--------------+-------+
|   id        | created at|      config        |      stats    |    message   | label |
+-------------+-----------+--------------------+---------------+--------------+-------+
| 7a3530f742  | 2018-06-03| {'n_neightbors': 7}| {'accuracy':  |     knn      |  None |
|             | 07:22:07  |                    |   0.8125}     |  classifier  |       |
+-------------+-----------+--------------------+---------------+--------------+-------+
| 9095c50d30  | 2018-06-03|   {'n_jobs': 6}    | {'accuracy':  | random forest|  None |
|             | 07:22:07  |                    |  0.9375}      |  classifier  |       |
+-------------+-----------+--------------------+---------------+--------------+-------+
```
Now after the creation of snapshots, we can perform checkout to a different version with the following command,

```
home:~/datmo-face-recognition$ # Run this command: datmo snapshot checkout <snapshot-id>
home:~/datmo-face-recognition$ datmo snapshot checkout 9095c50d30
```
Built using [dlib](http://blog.dlib.net/2017/02/high-quality-face-recognition-with-deep.html) and [face_recognition](https://github.com/ageitgey/face_recognition)

#### e. Listing runs and and reruning them
You can list the runs using the command,
```
home:~/datmo-face-recognition$ datmo run ls
+------------------------+------------------+---------+----------------------+---------+--------------------------------+
|        id              |     command      |  status |        config        | results |           created at           |
+------------------------+------------------+---------+----------------------+---------+--------------------------------+
|    0d0e315d5bc4a       | jupyter notebook | SUCCESS | {u'n_neightbors': 7} |    {}   | Tue Jul 03 12:42:01 2018 -0700 |
+------------------------+------------------+---------+----------------------+---------+--------------------------------+
```
Now, you can rerun any experiment for a particular run-id from the listed runs. 
```
home:~/datmo-face-recognition$ datmo rerun 0d0e315d5bc4a
```
