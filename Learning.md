
## Types Of AE
Types of Autoencoders:

1. Vanilla Autoencoders: The most basic type of autoencoders are vanilla autoencoders. Vanilla autoencoders are composed of an input layer, an output layer and one hidden layer in between. The hidden layer has fewer nodes than the input layer, which forces the autoencoders to compress the input data. 

2. Sparse Autoencoders: Sparse autoencoders are similar to vanilla autoencoders, but they include an additional regularization term that encourages the model to use only a small subset of the input nodes. This results in a more compact representation of the input data. 

3. Denoising Autoencoders: Denoising autoencoders are similar to vanilla autoencoders, but they are trained using corrupted input data. This forces the autoencoders to learn the structure of the input data and disregard the corruptions. 

4. Contractive Autoencoders: Contractive autoencoders are similar to sparse autoencoders, but they include an additional regularization term that encourages the model to learn a sparse, but also robust representation of the input data. 

5. Convolutional Autoencoders: Autoencoders that use convolutional neural networks (CNNs) to reduce the input dimensionality. 

6. Variational Autoencoders: Autoencoders that encode input data as a set of latent variables that are randomly sampled from a specific distribution.

7. Generative Adversarial Autoencoders: Autoencoders that are trained in an adversarial manner to generate new data.

### Two Main Categories of Generative Image Models:

 1. Non-Parametric:

Relies on matching images or image patches from a database.
Applications include texture synthesis, super-resolution, and in-painting.
Resources:
Texture Synthesis: Efros et al., 1999
Super-resolution: Freeman et al., 2002
In-painting: Hays & Efros, 2007

2. Parametric:

Involves learning parameters of a model to generate images.
Historically challenging for generating realistic natural images.
Recent progress includes:
Variational Autoencoders (VAEs): Kingma & Welling, 2013 (Known for blurry samples)
Diffusion Models: Sohl-Dickstein et al., 2015 (Iterative forward diffusion process)
Generative Adversarial Networks (GANs): Goodfellow et al., 2014 (Noisy and incomprehensible early results)
Laplacian Pyramid GANs: Denton et al., 2015 (Improved quality, but "wobbly" objects)
Recurrent Network-based Generators: Gregor et al., 2015
Deconvolutional Network-based Generators: Dosovitskiy et al., 2014
Limitations:

**Key Takeaways for a Deep Learning Engineer Interview**

Demonstrate a strong understanding of the fundamental concepts of generative image models.
Be prepared to discuss the strengths and weaknesses of different approaches, including VAEs, GANs, and diffusion models.
Highlight the challenges associated with generating high-quality and realistic images.
Discuss potential research directions, such as improving image quality, leveraging generative models for supervised tasks, and exploring new architectures.

**How To Visualize**

In the context of CNNs, Zeiler et. al. (Zeiler & Fergus, 2014) showed that by using deconvolutions and
filtering the maximal activations, one can find the approximate purpose of each convolution filter in
the network. Similarly, using a gradient descent on the inputs lets us inspect the ideal image that
activates certain subsets of filters (Mordvintsev et al.).

**DCGAN**

1. The first is the all convolutional net (Springenberg et al., 2014) which replaces deterministic spatial
pooling functions (such as maxpooling) with strided convolutions, allowing the network to learn
its own spatial downsampling. We use this approach in our generator, allowing it to learn its own
spatial upsampling, and discriminator.

2. Key Architectural Guidelines for Stable Deep Convolutional GANs

Convolutional Focus:

Replace pooling layers: Utilize strided convolutions in the discriminator and fractional-strided convolutions in the generator.
Minimize fully connected layers: Employ global average pooling or connect convolutional features directly.
Normalization:

Batch Normalization: Stabilize learning and prevent generator collapse.
Apply batchnorm to most layers, except for the generator output and discriminator input.
Activation Functions:

Generator: ReLU for most layers, Tanh for the output layer (for better color space coverage).
Discriminator: LeakyReLU (especially beneficial for higher resolutions).
Key Takeaways

Improve GAN stability and training efficiency: These guidelines are crucial for successful deep GAN training.
Convolutional architectures and efficient normalization: Play a significant role in successful deep GAN training.
Careful selection of activation functions: Significantly impacts model performance.

**Potential Interview Questions**

Why is it beneficial to replace pooling layers with strided convolutions in GAN architectures?
How does batch normalization help stabilize GAN training?
What are the advantages of using LeakyReLU in the discriminator?
How do these architectural guidelines contribute to the generation of high-quality images?

**DEDUPLICATION**

To further decrease the likelihood of the generator memorizing input examples (Fig.2) we perform a
simple image de-duplication process. We fit a 3072-128-3072 de-noising dropout regularized RELU
autoencoder on 32x32 downsampled center-crops of training examples. The resulting code layer
activations are then binarized via thresholding the ReLU activation which has been shown to be an
effective information preserving technique (Srivastava et al., 2014) and provides a convenient form
of semantic-hashing, allowing for linear time de-duplication . Visual inspection of hash collisions
showed high precision with an estimated false positive rate of less than 1 in 100. Additionally, the
technique detected and removed approximately 275,000 near duplicates, suggesting a high recall.