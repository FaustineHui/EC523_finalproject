# EC523_finalproject
 
## Task
In recent years, people have proposed and implemented a large number of methods for artificially synthesizing pictures and media files based on deep learning. Generative Adversarial Networks (GANs) in particular have brought huge quality improvements. GANs enable the possibilities to regenerate images as well as modify existing ones. Based on these functions, some practical software or programs are gradually developed, such as improving the clarity of pictures, or intelligently retouching pictures.

However, the technology can also be used for malicious purposes, such as generating fake profiles on social networks or generating fake news. Users could easily be confused by GAN-generated images because they may differ from real images by only a small amount. Therefore, it is urgently needed for automated tools that can reliably distinguish between authentic and manipulated content.

Naturally, our task is fake image detection: given an input image, the model output whether the image is authentic or generated.

## Model Mentioned
Xception, DenseNet, Spec(FFT), DCT

## Environment
Anaconda + Pytorch

## Approach
we propose to combine the two methods of learning spatial and frequency domain features together, i.e., to combine models that take these two approaches through Ensemble Learning, and create a method that take advantages from both spatial and frequency domain.

To start with, we begin by re-implementing well-performed detectors that belong to above two methods, to gain further understanding of what aspects of these different models can impact on the performance of GAN image detection. Detectors based on very deep networks that belong to the first method are introduced in reports. Detector from the second method of learning frequency domain features is a model that takes image spectrum as input. We also propose a new model by providing another type of spectrum input to this model.

## Dataset
The dataset comes from: [CNNDetection](https://github.com/peterwang512/CNNDetection)

## Averaged Result
Our full test data are available in our code repository. Here we take the overall average for our analysis.

| Averaged Accuracy | ProGAN 
(same category) | ProGAN \\(overall) | Different GANs \\(similar category) | Different GANs \\(overall) |
| ---- | ---- | ---- | ---- | ---- |
| Xception | 99.2 | 90.2 | 68.36 | 64.21 | 
| DenseNet | 73.4 | 60.23 | 54.09 | 50.93 |
| Spec | 83.8 | 74.03 | 55.81 | 49.15 |
| DCT-Spec | 87.4 | 76.74 | 56.72 | 51.37 |
| Ensemble | 98 | 86.99 | 66.87 | 55.34 |

From the table it's obvious that the accuracy of all models decrease as they move from same category in same GAN, to different category, to different GANs but similar categories, and to different GANs in different categories. In our data, even for the best performing Xception, ensemble learning (69.15%) still outperforms the corresponding Xception model (66.95%) in the fake category of sofa.

## Conclusion
Models perform best when tested on the same GAN within same category.

When they encounter unseen GANs, they are highly likely to still perform decently on similar categories, but may not work as well on unseen GANs and unseen categories.

Soft Ensemble Learning can boost overall performance based on each model’s capability. And it can also use some models' advantages to make up for others' disadvantages, as we've seen above for the Xception.

To further improve our method, models can be fine-tuned, more models can be added, data augmentation can be deployed. In conclusion, we prove that the Ensemble Learning can successfully take advantages from different models from different approaches, and make it more robust and generalizing to act as a universal GAN detector.
