# GAN_CIFAR
Following repository presents an implementation of Generative Adversial Network (GAN) written in PyTorch. Data used for model training comes from CIFAR10 dataset available through Torchvision.

# GAN
GAN's conception was primarly published in [Generative Adversial Nets](https://arxiv.org/abs/1406.2661) paper written by Ian J. Godefellow et al. 

Generative adversial network is a type of framework consisting of generative model $G(\mathbf{z}, \theta_G)$, where $\theta_G$ are aparameters of $G$, creating data based on random noise $\mathbf{z}$ and of discriminative network $D(\mathbf{x}, \theta_G)$ which returns probability that observation $\mathbf{x}$ comes from training set.

Both framework's parts learn synchronically during training process during which $D$ tries to guess whether observation $\mathbf{x}$ was taken from training set or generated by $G$. GAN's goal is to maximize the probability of $G$ labeling samples in a correct way. On the other hand $G$ tries to fool the discriminator which results in minimizing $\log(1 - D(G(\mathbf{z})))$.

Following minimax game can be summarized by value function $V(D,G)$:

$$\min\limits_{G} \max\limits_{D} V(D,G) = \mathbb{E}_{x \sim p_{data}(\mathbf{x})}[logD(\mathbf{x})] + \mathbb{E}_{\mathbf{z} \sim p_{\mathbf{z}}(\mathbf{z})}[log(1 - D(G(\mathbf{z})))]$$

where:

$p_{data}(\mathbf{x})$ - distribution of original dataset; 

$p_{\mathbf{z}}(\mathbf{z})$ -  distribution on input noise variables.

Authors of [Generative Adversial Nets](https://arxiv.org/abs/1406.2661) mention that the above equation should not be used in a direct way - on early phase of learning when $G$ generates observations obviously different from the training set, $D$ can classify them faultlessly as product of $G$. That could end up with saturation of $log(1 - D(G(\mathbf{z}))$ which indicates that a better way to train $G$ is to maximize $D(G(\mathbf{z}))$.
