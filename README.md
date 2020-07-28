## Shiba vs Jindo Breed Classification

### Motivation
After attending a online dog pet adoption events for rescues, I always heard the question of "what breed is s/he?". Unfortunately, the response by the rescue organization was "We aren't exactly sure", which is because they rescue dogs from many places. This motivated me to make a model that will be able to tell what breed a dog is just by using a simple image.

### Steps
1. Gathered and scraped image data from a simple google search of the two breeds (Shiba and Jindo) using Selenium and urllib packages
2. Quick manual filtering out of images that were not pictures of actual dogs (meaning pictures of drawings, stuffed animals, etc..) resulting in ~300 images for each breed.
3. Split up data into train, test, and validation sets
3. Data Augmentation in Keras generating 1800+ images.
4. Built a baseline convolutional neural network 
5. Applied transfer learning using a VGG16 model

### The Data

I gathered about 300 images for both classes. The augmented data consists of images that have been transformations through a combination of 20 or -20 degreen rotations, zooming in, and/or flipping. Below are images of the original data and the augmented data. These images look very similar but you can easily look out for a horizontal flipping.


![original data](/images/data_original_collage.png) 

----------

![augmented data](/images/data_augmented.png)


### Model

I created multiple CNNs with either 4 layers or 6 layers. I used only 5 or 10 epochs and tried different batches from 50 - 200. I saw that with batches too small, letting the model quickly learned the best way to minimze the loss function is by guessing one class. In the end I ended up going with a baseline model that had the same structure as an AlexNet with 8 layers. It had 5 convolutional and 3 fully connected layers utilizing dropout regularization for fixing overfitting. 



The final model I got is from using transfer learning on the VGG16. I froze the features from the model and added my own output layer for this specific classifcation of Shiba or Jindo. I got a final slightly underfit model with a test accuracy of 0.8333 and an F1-score of 0.8148. 


Confusion Matrix:




![confusion matrix](/images/confusion_matrix.png)



Here are some images that are properly classified

Properly classified:



![classified properly](/images/classified.png)



### Conclusion

The final model didn't end up only picking the dominate class, and also did equally well for identifying both classes. Since this is a CNN, it is hard to see what the model is doing when classifying the images.

Misclassified images:


![misclassified images](/images/misclassified.png)



To overcome this, a next step would be to use Grad-CAM to actually create a heatmap onto the image to see what is actually being visualized. Besides understanding what is being looked at, I can make a even better model by using transfer learning with a multiclass output rather than binary. This would make it much better for practical applications since the predictions wouldn't have the limited response of two breeds. 



### Github Contents and Materials

1. The notebook "image_scraper" has code for getting the images from Google.
2. The notebook "image_processing" has code for data augmentation process and visualizations for images
3. The notebook "cnn_notebook" includes all code for processing and modeling.



If you would like access to my data you can request it from this link:
https://drive.google.com/drive/folders/1pOl1wzzsvaJAofnFfEtv6x0Cus9B7NFv?usp=sharing
