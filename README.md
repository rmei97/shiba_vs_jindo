# Shiba vs Jindo Breed Classification

## Motivation
After attending some live dog pet adoption events for rescues, I saw that it's not uncommon that the breeds of the dogs are not known. The goal is to make a model that will be able to tell what breed a dog is just by a simple picture.

## Steps

1. Gather and scrape image data from a simple google search of the two breeds.
2. Quick manual filtering out of images that were not pictures of actual dogs (meaning pictures of drawings, stuffed animals, etc..) resulting in ~250 jindo and ~300 shiba images.
3. Data Augmentation in Keras to have enough data to actually run a neural network.
4. Build and run a convolutional neural network

## The Data

Below are collages of the originally scraped data and augmented data. The augmented data consists of images that have been transformations through a combination of 20 or -20 degreen rotations and zooming in.


Original
![original data](/images/data_original_collage.png)


Augmented
![augmented data](/images/data_augmented.png)

## Model

For now I created multiple CNNs with either 4 layers or 6 layers. I used only 5 or 10 epochs and tried different batches from 50 - 200. I saw that with batches too small, letting the model quickly learned the best way to minimze the loss function is by guessing one class.


The best base model so far is a 6 layer CNN with 5 epochs and 200 batches.


Metrics
![original data](/images/metrics.png)


Confusion Matrix
![confusion matrix](/images/confusion_matrix.png)


## Conclusion

The model here is still overfit, but has a test accuracy of 0.68913 and F1 score of 0.71648. This model thinks a lot of the shibas are jindos. Since the model uses a sigmoid activation layer, the misclassifcation may be happening because the model isn't getting enough signals to make it realize its looking at a Shiba.

Link to [Presentation Slides](https://docs.google.com/presentation/d/1c2fnI6nc2q_7AyAe_qc_ZstVhijFHI27bVRw1a2T38I/edit?usp=sharing)

I do not own any of these images an will provide a link to the data I collected in the future. 


## Next Steps

To make this model even better, I can get more data or even cleaner data, meaning more uniform images of the dog in focus. With more time I can add layers to do dropout regularization and batch normalization to help with the overfitting. Finally, I could use transfer learning with an AlexNet or VGG-19 which will probably yield even better results.


## Github Contents

1. The notebook "Image Scraper" has code for getting the images from Google.
2. The notebook "CNN Modeling" has code all the way from EDA to best build model. The notebook also include multiple other manually model tests


