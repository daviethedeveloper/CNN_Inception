## Introduction:
In the pursuit of improved sign recognition for automatic cars, Convolutional Neural Networks provide a powerful and consistent means for computers to identify street signs. With automatic cars on the horizon, accurate modules exist to recognize signs in Germany. These modules, in turn, can propel GehirnWagen ahead of the pack, positioning them as the leading innovators in the automatic car market.

## Approach:
Our AI team has developed several modules to achieve optimal average results. These modules involve building models from scratch, in addition to utilizing transfer learning with modules that have undergone thorough study and research. Multiple models and iterations of each model type were tested to determine the best averages and which model demonstrated the most consistent ability to address the presented problem. Among the experimented models, those utilizing transfer learning included InceptionV3 and VGG-16. One side effect of using previously trained models is that they tend to lack certain desired recognition.

In the case of the aforementioned models, they were primarily trained for face recognition rather than our intended target of signs. Utilizing the existing architecture but training from scratch allows the model to learn how to identify traits specific to signs. The difference after training a model without retraining the InceptionV3 base and after retraining is noticeable, with an over 30% increase in accuracy.

<img src="Images/acc_nt.png" width="500" height="auto" alt="Image1">
<img src="Images/acc_wt.png" width="500" height="auto" alt="Image2">


[The y axis shows accuracy between 0 and 1]
Due to this discrepancy, all models were retrained on the specific dataset that exclusively includes the target types of images.

## Iterating over the Model:

After the models were trained, it was necessary to go through the test data and confirm what the model was able to accurately predict and identify areas where it struggled. Through this process, the model significantly improved its ability to correctly identify street signs.

<img src="Images/comparison.png" width="500" height="auto" alt="Image5">

The need at this point was to identify what the model consistently missed between model iterations. Example photos of signs that were consistently misclassified are shown below. These photos illustrate a few issues that needed to be addressed with the model.

<img src="Images/original_pictures.png" width="500" height="auto" alt="Image7">

A theme that was difficult for the model to accurately predict was dark photos. An additional issue for the model was signs that were covered in graffiti. These were pressing issues that needed to be addressed for the car to drive safely at night or in areas with less-than-desirable signs. 

## Data Augmentation

As much of the training data is uniform somewhat in nature, data augmentation was exposed to as many unique photos as possible, data augmentation was used to slightly augment photos. This results in a better generalized model that can predict with higher accuracy on the average. The augmentations that were used for training that produced the final model included stretching, shrinking, zooming in and out, shearing and flipping the photo over the y axis. This introduces irregularities that trains the module to find more patterns from more angles. 

Brightness in photos being one of the largest if not the largest challenge for the model, brightness was randomly adjusted for each photo as the model trained. Through generations the model could then see the same photo bright as though it was midday and then in the next generation it could be much darker simulating night time. The results with this technique were effective as it steadily dropped the number of dark photos that were misclassified.

Another issue for training the model was graffiti on signs. In order to combat an algorithm was written as a data augmentation to randomly add lines in a photo. This produces a random synthetic graffiti for the model to learn from.

<img src="Images/augmented_images.png" width="500" height="auto" alt="Image4">

## Pre-Processing

Using data exactly as it is found in the training data can lead to a less generalized model.. There were several preprocessing steps in order to make sure the images were best suited for the models to use. Over iterations it was found that as a preprocess step, it was important to grayscale the photos as it allowed for greater consistency.


Additionally, we introduced adjustments by intentionally blurring certain images. This modification aims to enhance the model's training by exposing it to variations in image clarity, thereby improving its ability to handle test images that are predominantly blurry. This proactive measure ensures that the model becomes more adept at recognizing and interpreting signs even in less-than-optimal visual conditions, contributing to its overall robustness and performance.

## Analysis
Overall as a final result the best model that was trained had an overall f1 score of 98%. With these results the types of images that were incorrect were typically blurry or had difficult lighting. Dark photos still being an issue is something that needs to be addressed to a higher degree as it is not sensible to take pictures of the signs at night with a flash. 

## Confidence
We need to be practical in acknowledging that a majority of the images are sourced from dashcams, often capturing multiple shots of the same sign with slight variations. While on the road, it's essential to anticipate potential anomalies since signs may be entirely covered or have elements that deviate from the original. The noteworthy capability of both humans and computers lies in the ability to identify the sign's shape and purpose, even when compromised by graffiti or stickers. The objective is to assist the computer in recognizing these alterations and emphasizing the key details of each sign, even when obscured by external elements (refer to the accompanying pictures below).

<img src="Images/altered_images.png" width="500" height="auto" alt="Image3">

Following a comprehensive analysis, we've determined that this dataset may not be the optimal choice for accurately predicting road signs, particularly for ensuring a 100% confidence level in the system's understanding. This is particularly evident in instances where speed limit signs were not well-recognized, potentially impacting driving safety and the occurrence of accidents. To address this issue proactively, it is advisable to incorporate additional data featuring road signs from Germany in diverse contexts. Factors such as climate, weather conditions, sign damage, light (night and day), and environmental elements (such as tree leaves obstructing parts of the signs) should be considered to enhance the dataset's robustness.

For an extended period, signs have served as crucial aids, enhancing our human ability to comprehend instructions and concepts effectively. By diligently following these steps, we have strong confidence that future models will exhibit heightened precision, mitigating errors caused by picture blurriness and external factors influencing sign clarity. The key lies in a meticulous plan that considers various options for adding diverse pictures, ensuring a comprehensive training set that guards against inadequate learning.

<img src="Images/distribution_imagetypes.png" width="500" height="auto" alt="Image6">

A notable challenge involves the irregular distribution of pictures across different classes. It's understandable that more common signs like stop or priority road signs may naturally outnumber less frequent ones like slippery road signs. Nevertheless, it is imperative for our neural network to gather sufficient information to perform adeptly on less encountered signs. Many errors observed stem from these less popular signs, posing potential dangers if the system fails to recognize them when encountered by drivers. Striking a balance in the dataset to encompass a wide range of signs is essential for the system's overall effectiveness and safety.
