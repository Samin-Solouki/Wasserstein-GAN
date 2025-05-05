# Wasserstein-GAN
# Stabilizing GAN Training with Wasserstein Distance

Implements Wasserstein distance for meaningful gradients even when distributions do not overlap


##  Project Level:

**Advanced (Deep Learning, GANs, PyTorch)**

##  Project Highlights

* Tackles major GAN issues: *mode collapse*, *vanishing gradients*, and *training instability*
* Implements Wasserstein distance for meaningful gradients even when distributions do not overlap
* Uses a *Critic* instead of a *Discriminator* for scalar scoring
* Applies label smoothing and learning rate tuning for stable convergence
* Trains on image dataset with visual sample outputs and loss curves

##  Project Description

This project implements a Wasserstein Generative Adversarial Network (WGAN) to generate images with improved training stability compared to traditional GANs. It utilizes the Wasserstein distance as the loss function, providing smoother gradients and reducing mode collapse. The generator and critic are trained in a min-max game where the critic estimates the Wasserstein distance between real and generated data distributions.

##  Objective

* Generate realistic images using a GAN architecture with enhanced training dynamics.
* Overcome traditional GAN problems: unstable convergence, mode collapse, and vanishing gradients.
* Evaluate the effectiveness of WGAN using visual inspection and loss curve analysis.

##  Data Collection

* Images are preprocessed and normalized before training.

##  Preprocessing & Feature Extraction

* Images resized and scaled to the \[0,1] range.
* Applied normalization using dataset mean and standard deviation.
* Used image transformations to augment data (if applicable).

##  Data Augmentation (if applicable)

* Applied label smoothing to reduce overconfidence in the critic:

  * Real labels set to 0.05, fake labels set to 0.95.

##  Model Architecture

### Generator:

* Uses multiple `ConvTranspose2d` layers for upsampling.
* Activations: ReLU for hidden layers, Tanh for output.
* Batch Normalization used for training stability.

### Critic (Discriminator replacement):

* Uses `Conv2d` layers with LeakyReLU.
* No sigmoid activation in the output.
* Outputs a scalar score estimating the realness (Wasserstein score).

##  Training & Evaluation

* **Optimizer**: RMSprop / Adam with tuned learning rates:

  * Critic LR: 0.00001
  * Generator LR: 0.0002
* **Epochs**: 60
* **Loss Functions**:

  * Wasserstein loss (no sigmoid, no binary cross entropy)
* **Critic trained more iterations per generator step** (5:1 ratio)
* Weight clipping used for enforcing Lipschitz constraint

### Techniques for Stability:

* Weight clipping for Lipschitz continuity
* Label smoothing to stabilize critic
* Gradient penalty (if implemented)
* Loss tracking and visual inspection

##  Results

* Generator learns to produce realistic and diverse samples
* Training losses show stable convergence after \~7 epochs
* Visual improvement of generated images over epochs (see below)
* Avoided mode collapse and ensured consistent gradient flow

* Generated images- Epoch 59:
![image](https://github.com/user-attachments/assets/a94bc12b-c2c2-482e-bc5a-cadd40cf177b)
* FID score during training"
![image](https://github.com/user-attachments/assets/055fbdc2-9d63-424e-b905-4e21db35c077)

##  Conclusion

The WGAN model demonstrated significant improvements over traditional GANs by addressing vanishing gradients and mode collapse. By using the Wasserstein distance and modifying the training setup (e.g., critic overtraining, label smoothing), the model achieved stable convergence and generated high-quality images.

##  Future Work

* Replace weight clipping with gradient penalty (WGAN-GP)
* Explore different architectures (e.g., DCGAN, ResNet blocks)
* Use larger and more complex datasets for generalization
* Evaluate using metrics like IS, and PPL

---

آیا می‌خواهی فایل `README.md` آماده و قابل دانلود برایت بسازم؟
