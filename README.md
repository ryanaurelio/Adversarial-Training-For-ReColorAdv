# Adversarial Training For ReColorAdv

## Description
The idea of this defense is to use an adversarial training to defend against the ReColorAdv attack. In the training process of a model, ReColorAdv attack will be performed to the current state of the model for each batch. First, a model will be generated using ***model_generator***. Then the ReColorAdv attack will be applied to this generated model using ***model_attack***. Lastly, ***model_defense*** will try to defense this attack using an adversarial trqining.

## Setup
The setup that is used in this study.

| Paramteres       | Value                                            |
|------------------|--------------------------------------------------|
| Model            | ResNet                                           |
| Dataset          | CIFAR10                                          |
| Transformation   | Pad by 4, random flip and crop into 32x32 images |
| Batch size       | 100                                              |
| Number of epochs | 10                                               |
| Learning rate    | 0.001                                            |
| Loss Function    | Cross Entropy Loss                               |
| Optimizer        | Adam                                             |

## Implementation
First, the data is loaded without any transformation. A model then will be trained on the CIFAR10 dataset and the adversarial samples that is generated using the ReColorAdv, meaning one image will produce two inputs. For example, 1 batch consits of 100 images. These 100 images will be used to produce the attack to the current model state. There are now 100 normal images and 100 adversairal images. These 200 images will then be transformed using the transformation function defined above. Next, these images will be passed onto the model.

## Results
### Base model
| Test set           | Accuracy |
|--------------------|----------|
| CIFAR10 test set   | 0.8033   |
| Adversarial sample | 0.3609   |
### Defended model
| Test set           | Accuracy |
|--------------------|----------|
| CIFAR10 test set   | 0.7641   |
| Adversarial sample | 0.5989   |
