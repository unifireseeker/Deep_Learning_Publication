# General Deep Learning

## Index

### 1 - Training Dynamics of Neural Networks

- 1.1:	Understanding the difficulties of training deep feedforward Neural Networks - [2010][tr_dyn]   
- 1.2:	Exact Solutions to the Non-Linear Dynamics of Learning in Deep Linear NNs - [2013][exact_sol]
- 1.3:	On the Learning Dynamics of Deep Neural Networks - [2018][lr_dyn]

### 2 - Deep Learning Milestones
- 2.1:	Rectified Linear Units Improve Restricted Boltzmann Machines – ReLU - [2010][relu]
- 2.2:	A Simple Weight Decay Can Improve Generalization - [1991][weight_decay]
- 2.3:	Dropout: A Simple Way to Prevent Neural Networks from Overfitting - [2014][dropout]
- 2.4:	BN: Accelerating Deep Network Training by Reducing Internal Covariate Shift - [2015][batchnorm]
- 2.5:  How does Batch Normalization help Optimization? - [2018][batchnorm2]
- 2.6:	An overview of gradient descent optimization algorithms - [2016][grad_desc]

### 3 - Generalization Phenomena
- 3.1:	Generalization gap in large batch training of neural networks - Train longer, generalize better - [2017][generaliz]

---

[//]: # (General Links)
[medium]: https://towardsdatascience.com/deep-convolutional-neural-networks-ccf96f830178
[general_dl]: https://github.com/Udacity-PyTorchChallenge-Students-Group/Deep_Learning_Publication/tree/master/General_DL
[cnns]: https://github.com/Udacity-PyTorchChallenge-Students-Group/Deep_Learning_Publication/blob/master/CNNs

[//]: # (General DL Links)
[tr_dyn]: http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf
[exact_sol]: https://arxiv.org/pdf/1312.6120.pdf
[lr_dyn]: https://arxiv.org/pdf/1809.06848.pdf
[relu]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.6419&rep=rep1&type=pdf
[weight_decay]: https://papers.nips.cc/paper/563-a-simple-weight-decay-can-improve-generalization.pdf
[dropout]: http://jmlr.org/papers/volume15/srivastava14a.old/srivastava14a.pdf
[batchnorm]: http://proceedings.mlr.press/v37/ioffe15.pdf
[batchnorm2]: https://arxiv.org/pdf/1805.11604.pdf
[grad_desc]: https://arxiv.org/pdf/1609.04747.pdf
[generaliz]: https://arxiv.org/pdf/1705.08741.pdf


## 1.1 Understanding the difficulty of training deep feedforward neural networks
*Xavier Glorot - Yoshua Bengio*  

#### What problems are solved?
- Difficulty on training deep networks - Converge
- Understand the effect of different activation function: Sigmoid and TanH

#### What are the key innovations?
- They propose a distribution to initialize the weights of a network to increase the performance and the convergence during training
- They monitor the gradients and the activations layer-wise per iteration during training to track the evolution
- They detect the **vanishing/exploding** variance of the back-porpagated gradients

#### What are the conclusions?
- It is better to keep layer-to-layer transformations such as the activations and the gadients flow well (i.e, Jacobian ≈ 1)
- Sigmoids should be avoided when initializing from small weights - they yield to quickly saturation of the first hidden layer
- Having different magnitudes of the gradients at different layers may yield to ill-conditining slow training  

... 

---

## 2.4. Batch Normalization - Accelerating Deep Network Training by Reducing ICS
*Sergey Ioffe - Christian Szegedy*  

#### Summary
We can understand every layer as a subnetwork that receives a changing input from the layer (subnetwork) that precede it. The change in the distribution of the network activations is called the internal covariate shift, and it could yield to exploding/vanishing gradients if the learning rate is not carefully set.
Furthermore, it is well known that networks converge faster if the dataset is whitened (normalized and decorrelated). Why don’t use the same principles for the inputs of every layer? 

#### Conclusion
By adding these extra layers that normalize the output of each layer preceding it by using the statistics of each mini-batch, the problem of the vanishing gradient is heavily overcome, and the training is potentially faster since we are able to use higher learning rates without losing convergence properties.

---

## 2.5. How does Batch Normalization help optimization?
*Santukar, Tsipras, Ilyas*

## Summary
The popular belief of why BN works has been always the fact that it reduces the internal covariate shift by adding new layers that control the first two moments (mean and variance) of the distribution of layers’ input. However, the authors find cases where BN actually increases the covariate shift. Therefore, its great success must be attributed to something else. 
Authors claim that the key of the success is the change in the landscape loss function to be more “smooth”. This way, the gradients are more predictive and allows for the use of higher learning rates.

## Conclusion
By reparametrizing the underlaying optimization problem when including the extra parameters of the batch normalization layers, we are modifying the underlying problem in a way which the calculated gradients are closer to the real gradients. Thus, the learning rate could be increase and the whole training be accelerated.
 
...
