# Shoe Design using Generative Adversarial Networks

**Author: [Hoang Le](https://github.com/hminle) - [Hoang Nguyen](https://github.com/hoangnguyen3892)**

This repository developed a Generative Adversarial Nets (GANs) to design and generate new shoes images. Many improvement techniques were implemented to enhance the performance of the model as well as the quality of the output.

This was also used as a final project for the course __Deep Learning for Visual Recognition__ Spring 2017 semester.

For more information, you guys can read our report.

### Directory structure:

```
shoe-design-using-generative-adversarial-networks
│   README.md
|   report.pdf
|
|--- data: original dataset
| 
|--- experiment
|
|--- results


```

In **experiment** directory, you can find our notebooks which define DCGAN Networks and some modification.

### Dataset

In this project, we consider shoes dataset: [UT Zappos50K](http://vision.cs.utexas.edu/projects/finegrained/utzap50k/)
The dataset consists of over 50,000 images
Sneaker type is dominant in the dataset (12856 images), so we decide to use only sneakers' images as the main data source.

We put the data dir like this: 
```data/ut-zap50k/Shoes/Sneakers_and_athletic_shoes/```

### Methods
**Baseline Model**
- All pooling layers are replaced with strided convolutions (discriminator) and fractional-strided convolutions (generator)
- Batch normalization is applied 
- All fully connected layers are removed.
- ReLU is used for all layers of the generator, except Tanh is used for the output, and LeakyReLU is used for all layers of discriminator.
![dcgan architecture](https://cdn-images-1.medium.com/max/1000/1*39Nnni_nhPDaLu9AnTLoWw.png "DCGAN Architecture")

**Improvement Techniques**
1. Objectives:
    - To generate higher-resolution images 
    - To avoid the case that D over-perform G
2. Detail implementations:
    - Use a modified loss function: 
	        min[log(1-D)]  max[logD] 
    - Use a spherical noise: the noise will be sampled from a Gaussian distribution.
    - Use one-sided label smoothing: make the discriminator target output from [0=fake image, 1=real image] to [0=fake image, 0.9=real image]. 
    - Freezing: Stop update D when loss D < 0.7 loss G.

### Results

**Experiment 1**
Pure DCGAN with spherical noise

![ex1](https://user-images.githubusercontent.com/16201681/28861890-ef380692-779d-11e7-8466-630ef63dfc3a.png)

**Experiment 2**
- Normalized input
- Weight decay
- Modified loss

![ex2](https://user-images.githubusercontent.com/16201681/28861892-ef39dde6-779d-11e7-97fc-04641def50c7.png)

**Experiment 3**
- Normalized input
- Weight decay
- Sided-label of 0.9 for real data

![ex3](https://user-images.githubusercontent.com/16201681/28861891-ef38fcaa-779d-11e7-800e-500074f9e12f.png)

**Experiment 4**
- Normalized input
- Weight decay
- Sided-label of 0.9 for real data
- Freezing: Stop update D when loss D < 0.7 loss G.

![ex4](https://user-images.githubusercontent.com/16201681/28861893-ef3a2cce-779d-11e7-9c01-033edc4aee19.png)

### Some Conclusions

- GANs is extremely unstable and hard to train.
- The common case is that the discriminator became too powerful and was able to easily make the distinction between real and fake images while the generator was still dumb.
- With some methods proposed, the results from the generative model were improved.
- There are some artifacts that we can easily observe.

### Requirement

- [Pytorch](pytorch.org)
- [PyTorchNet](https://github.com/pytorch/tnt)
- [torch-vision](https://github.com/pytorch/vision) 

### Acknowledgments

Thank [Du Phan](https://github.com/fehiepsi) for your guidance, without it we cannot finish this project.

### References
See our report for detail.
