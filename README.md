# ***Introduction to Vertical Federated Learning***
## **Background**

### Vertically Partitioned Data

Often data exists in silos. This can be the case within an organization or among multiple organizations. In each case, the feature of a unique sample is distributed among multple datasets held by different parties. Exchanging data allows the parties to leverage a more complete feature set, thus enhancing the performance of the system. However, privacy restrictions often prevent the parties from doing so. 

### Vertical Federated Learning

Inspired by this limitation, [Vertical Federated Learning](https://blog.openmined.org/federated-learning-types/) (VFL) was introduced. VFL involves training a joint model on data that has features partitioned accross multiple datasets without explictly exchanging the features among parties.
<p align="center">
<img width="433" alt="Screen Shot 2021-09-28 at 5 41 20 PM" src="https://user-images.githubusercontent.com/34798787/135169716-27e0e6a1-1d45-421d-882a-27241805b401.png">
</p>

### Use Case

A logical application of vertical federated learning is in the financial services industry, where several instituions hold credit data for the same individual. Although there is an inherent benenfit of exchanging data, instituions are restricted from doing so. To explore this scenario, we will be using the [Home Credit Default Dataset](https://www.kaggle.com/c/home-credit-default-risk/overview). This dataset contains features about credit applicants drawn from Home Credit's internal operations as well as data from the Credit Bureau. 
<p align="center">
<img width="759" alt="Screen Shot 2021-09-28 at 3 42 48 PM" src="https://user-images.githubusercontent.com/34798787/135170454-f937a987-0dcf-4b3a-a9f9-1bcbeac3bc9f.png">
</p>

In order to apply VFL to this dataset, we have vertically partitioned into two datasets based on the origin of the features, Home Credit or the Credit Bureau. In total, there are ~300000 samples with corresponding labels.  The task at hand is to predicting future payment behavior of clients. 
<p align="center">
<img width="487" alt="Screen Shot 2021-09-29 at 1 40 53 PM" src="https://user-images.githubusercontent.com/34798787/135320845-db616df5-a9bd-4a26-a64d-fdf5c0ba3dcf.png">
</p>

### Tools
In order to perform VFL, data and computation need to be distributed amongst the remote machine(s) of each party. However, deep learning frameworks like PyTorch and TensorFlow do not offer this functionality of the box. Fortunately [PySyft](https://blog.openmined.org/tag/pysyft/), a Python library for secure and private Deep Learning, extends both PyTorch and Keras to provide tools to perform VFL.
## **Demo Overview**
In the following demo, VFL is used to train a joint model between Home Credit and the Credit Bureau to predict whether or not a credit applicants will default using PyTorch and PySyft. During this process, only abstract representations of features are shared thus eliminating the need to explictly exchange features. When coupled with differential privacy, VFL provides a robust solution to privacy preserving AI. 

The follwing demo contains three sections: 
1. **Data Preparation**
    *  Define Vertical Dataloader 
    *  Find correspondences with Private Set Intersection

2. **Model Preparation**
    * Define Sub Model 
    * Define Split Neural Network

3. **Training and Validation**
    * Define train and validation loop
    * Interpret results
