# Shiba vs Jindo Breed Classification

## Motivation
After attending some live dog pet adoption events for rescues, I saw that it's not uncommon that the breeds of the dogs are not known. The goal is to make a model that will be able to tell what breed a dog is just by a simple picture.

## Steps

1. Gather and scrape image data from a simple google search of the two breeds.
2. Quick manual filtering out of images that were not pictures of actual dogs (meaning pictures of drawings, stuffed animals, etc..) resulting in ~250 jindo and ~300 shiba images.
3. Data Augmentation in Keras to have enough data to actually run a neural network.
4. Build and run a convolutional neural network

## The Data

![Data Distribution](/images/pre_gen_distribution.png)

Again the number of scraped data points is ~250 for jindo and ~300 for shiba. The augmented data consists of images that have been transformations through a combination of 20 or -20 degreen rotations, zooming in, and/or flipping. Below on the left are some original scraped images and on the right are those images with a simple horizontal flip augmentation and slight color changing.


![original data](/images/data_original_collage.png) ![augmented data](/images/data_augmented.png)


After all the augmentations, the classes were balanced and had ~1150 images each class.

![post-gen distribution](/images/post_gen_distribution.png)


## Model

For now I created multiple CNNs with either 4 layers or 6 layers. I used only 5 or 10 epochs and tried different batches from 50 - 200. I saw that with batches too small, letting the model quickly learned the best way to minimze the loss function is by guessing one class. I've also attempted to do transfer learning, but couldn't get it to implement it right since I got wrong numbers. Instead what I did was make a neural net that had the same structure as an AlexNet with 5 convolution layers and 3 fully connected. The final model I arrived at used a learning rate of 0.001, a dropout rate of 0.1, 10 epochs and 260 batches. This final model was the best because of a high accuracy and only a slightly underfit model as opposed to the highly overfit models I first made.


Metrics:

![original data](/images/metrics.png)




Confusion Matrix:



![confusion matrix](/images/confusion_matrix.png)


Properly classified:



![classified properly](/images/classified.png)

## Conclusion

The final model didn't end up only picking the dominate class, and also did equally well for identifying both classes. Just by inspection on the misclassified images and using some prior knowledge, it seems that the model is having trouble with identifing mixed breeds. The image in the middle and the bottom left might have a mix of a corgi or pitbull. 

![misclassified images](/images/misclassified_matrix.png)

Link to [Presentation Slides](https://docs.google.com/presentation/d/1c2fnI6nc2q_7AyAe_qc_ZstVhijFHI27bVRw1a2T38I/edit?usp=sharing)


## Next Steps

To make this model even better, I can get more data or even cleaner data, meaning more uniform images of the dog in focus. With more time, fully properly implementing the transfer learning with AlexNet will probably yield even better results. There are already models for dog breed classifications like for the Stamford dog dataset and if I were to apply those models with my data, it would output a percentage of what the dog seems to be which would address my current models problem of trouble with mixed-breeds. Moreover, this model is a blackbox in that there isn't a way to tell what exactly is going on to produce the output, but by using a method called Gradient-weighted classification activation map (Grad-CAM), then it's possible to see what the machine is focusing on when looking at these images.

## Github Contents

1. The notebook "Image Scraper" has code for getting the images from Google.
2. The notebook "cnn_notebook" has code all the way from EDA to best build model. The notebook also include multiple other manually model tests
3. The notebook "transfer_learning" has everything in the cnn notebook, but also has code for attempting to do transfer learning

