# Go Home Discriminator, Your Drunk /  Fine Tuning with Discriminator Networks

In this repository we look at fine tuning generated images from GANs using the discriminator network. The idea is to tune the generated image such that the discriminator is more likely to predict it as a real image. We go about this in two ways. The first method is to generate an image with the generator network and then fine tune the pixels with the discriminator loss. The second method is to fine tune the input vector, Z, to the generator. As suggested by the title, the discriminator can be very easily fooled (in some cases). When fine tuning the pixels, the discriminator can be fooled with extremely small changes. Surprisingly, fine tuning the Z vector can actually produce more realistic images. This result is difficult to quantify so we have included pictures to support this claim. When training on the Celeb Dataset, Images with patchy hair or glasses tend to either remove the patches or fill in the missing spaces.

## Similar Work

The idea of tuning images steams from work in Style Transfer and Fooling Neural Networks. The predominate papers in these areas are [Image Style Transfer Using Convolutional Neural Networks]( http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf) and [Deep Neural Networks are Easily Fooled: High Confidence Predictions for Unrecognizable Images](https://arxiv.org/pdf/1412.1897.pdf). Our GAN implementation is taken from [here](https://github.com/shekkizh/WassersteinGAN.tensorflow). To get a list of dependencies see that page. We test our method on Wasserstein GANs because of their recent success.

## Fine Tuning Pixels

![](logs/images/image_iterator_2000.png)
![](logs/images/image_iterator_plot.png)

As seen in the photos and error plot. It is extremely easy to fool the discriminator with very slight changes in pixels. This is consistent with the results seen in Fooling Neural Network texts. I was hopeful that this would not be the case. Training GANs is dramatically different then training classification networks and it seems reasonable to hope that the discriminator would be more resistant to adversarial examples. Alas this does not appear to be the case.

## Fine Tuning Z vector

![](logs/images/z_iterator_500.png)
![](logs/images/z_iterator_plot.png)

Fine tuning the Z vector produces some interesting results. It appears to degrade images in a few cases however in those with very little structure there is a dramatic improvement. Images with almost no clear face began to take on eyes and textured skin. It required playing with the learning rate and number of iterations to get these results. Too few steps and there is almost no change in the image. Too many steps and the resultant image is far from the original.

More images!

Before
![](logs/images/generated_z_iterator.png)

After
![](logs/images/generated_z_iterator_after.png)

Difference
![](logs/images/generated_z_iterator_dif.png)

## Conclusion

- Poor images sampled from a GAN can be fine tuned to become more realistic.
- Discriminators are just as susceptible to adversarial examples as classification networks.
- My discriminator has had too much to drink and are therefore MUST GO HOME.


