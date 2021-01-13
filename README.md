# Accountable Federated Learning

This repository is the implementation of the paper 'Accountable Federated Learning against Local Poisoning Attacks'. 

We are clearning up the source code, and the PyTorch and MindSpore version will be uploaded as soon as possible after the corresponding paper is accepted.

## Requirements

To install requirements:

```setup
pip install -r pip-requirements.txt
```

## Training and Evaluation

###### Note that the defense mechanism works on each epoch of the federated learning; thus the training and testing stages are merged into the same script. To evaluated the effectiveness of the proposed the scheme, run this command:

```train
python main.py --n_device=20 --n_attacker=0.2 --dataset=mnist
```

> The hyper-parameter n_device is the number of devices in the federation, and the scheme simulates the federated learning process with serial training.
> The optional dataset can be mnist (MNIST), cifar (CIFAR-10), imdb (IMDB) or sst (SST-5), and n_attacker is in range (0,1), which indicates the percentage of attackers in the client.


## Comparision

To see the accuracy gains with the FedAvg algorithm that has no attacker, run:

```eval
python fedavg.py --n_device=20 --n_attacker=0.2 --dataset=mnist
```

> It is noted that for a pair comparision, the FedAvg with no attacker leads to less devices.
> For example, the number of devices is 8 in the federation of the above command line.

To see the defense effect with the FedAvg algorithm that the same number of attackers in the experiment, run:

```eval
python fedpoi.py --n_device=20 --n_attacker=0.2 --dataset=mnist
```

> The output Success Attack Rate means the probability that an image with attacked label is predicted as poisoned label.

> The Accuracy means the precision of the federated model on the standard test set after the learning process.

## Results

Our scheme achieves the following performance :


| Dataset | # of devices | # of attackers | Traceability Rate | Success Attack Rate | Accuracy |
| ------- |--------------| -------------- | ----------------- |-------------------- | -------- |
|  MNIST  |     20       |      2         | 100%              |     0.64%           |  96.64%  |
|  MNIST  |     20       |      6         | 100%              |     0               |  96.59%  |
|  MNIST  |     20       |      10        | 100%              |     0               |  95.93%  |
|  MNIST  |     20       |      14        | 100%              |     0               |  95.24%  |
|  MNIST  |     20       |      18        | 100%              |     0.37%           |  94.15%  |
|CIFAR-10 |     10       |      2         | 100%              |     0.53%           |  77.32%  |
|CIFAR-10 |     10       |      6         | 100%              |     0.10%           |  76.43%  |
|CIFAR-10 |     10       |      10        | 100%              |     0.91%           |  73.70%  |
|CIFAR-10 |     10       |      14        | 100%              |     3.45%           |  70.89%  |
|CIFAR-10 |     20       |      18        | 100%              |     5.98%           |  68.03%  |

