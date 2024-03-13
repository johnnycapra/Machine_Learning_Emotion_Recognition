# Machine_Learning_Emotion_Recognition
Code and presentation by Johnny Capra, Lucas Chacon, Laura Dudley, and Ian Morrison 

## Introduction 

For our final project, we decided to work with images and computer vision to train a machine learning model.  One of the most common applications of computer vision is facial detection, which is utilized in everything from digital cameras (remember those?) to smartphone security and social media tagging. We wanted to take this element of computer vision a bit further by trying to train a machine learning model to identify emotions in images of faces. While humans in general are pretty good at recognizing facial emotions, it can be challenging for autistic and other neurodivergent people to do so without extra effort and training. Since humans can learn how to better identify emotions by taking patterns and extrapolating from those patterns, the process seems well designed for a machine learning model too.

## Dataset

We found a large dataset of black & white images of faces (https://www.kaggle.com/datasets/chiragsoni/ferdata/data) depicting various emotions: anger, disgust, fear, happiness, sadness, surprise, and neutral or no emotion and used it to train our model. The composition of these images was based off a 2013 dataset prepared by Pierre-Luc Carrier and Aaron Courville as part of a research project (https://datarepository.wolframcloud.com/resources/FER-2013). 

Our dataset had over 35,000 images depicting just faces, centered in the image, and without extraneous other objects in the image. The faces are centered and without extraneous objects in the image. The images are also uniform in dimension - 48 pixels by 48 pixels - and in black & white. 

## Training and Refining Our Model

The model was run with 3 convolutional layers, with a max pooling layer after each convolutional layer. 
**Layer 1:** applied filters and specified shape & grayscale channel
**Layer 2:** applied twice as many filters to previous layer
**Layer 3:** applied 4 times as many layers as first layer
The max pooling layers reduced the spacial dimensions and extracted the most important features of each layer.
**Flatten Layer:** This layer flattens the 3D output tensor from the convolutional layers into a 1D tensor, which can be fed into the subsequent fully connected layers. 

Essentially, the image passes through convolution layers, with the global average pooling giving single value, weighted summation (weighted importance), normalization, and visualization heat map of activation values over input image.

The final dense layer consists of 7 neurons, each representing one of the classes in a classification task (e.g., emotions). The activation function used here is sigmoid, which is suitable for multi-label classification tasks.

The majority of the images (80%) were used for training, with the remaining 20% used for refining the model and testing the model after the initial training. Using Tensorflow and Keras, we trained the model using a convolutional neural network. This model was then tuned using a Keras tuner called Hyperband.

## Using Heatmaps to Visualize the Model
![cam_angry_2](https://github.com/johnnycapra/Machine_Learning_Emotion_Recognition/blob/main/output/cam_angry_2.jpg) ![cam_happy_2](https://github.com/johnnycapra/Machine_Learning_Emotion_Recognition/blob/main/output/cam_happy_2.jpg) ![cam_sad](https://github.com/johnnycapra/Machine_Learning_Emotion_Recognition/blob/main/output/cam_sad.jpg)

We generated heatmaps showing the areas focused on by the model, which give a great visual representation of the way the model learned to focus on the areas of a face with the most information. Since expression is conveyed by a combination of eyes, eyebrows, lips and even the nose, it’s interesting to see the way the model learned to focus on these elements after 3 convolutional layers.


## Successes and Challenges

After the model was trained and tuned, we were able to get our test to about 85% accuracy for some emotions, however the process was extremely time-consuming and we ran into several issues along the way. Other emotions were not identified well, which probably could be resolved with more epochs, or by shuffling the data.
We did not shuffle our data, so the model was trained in the order the files were presented in the training folders. This could affect the model in several ways: 

_Sequential Bias:_ If the training data is presented to the model in a fixed order without shuffling, the model may develop a bias towards patterns or trends present in the data sequence. For example, if similar instances are grouped together in the dataset, the model might learn to prioritize certain patterns over others, potentially leading to overfitting on specific subsets of the data.
_Learning Dynamics:_ The order in which data is presented can influence the trajectory of the model's optimization process. 
_Generalization Performance:_ The order of input data can impact the model's ability to generalize to unseen examples. If the training data is presented in a biased order that does not adequately represent the true distribution of the data, the model may struggle to generalize well to new, unseen instances.

## Conclusion and Potential Applications
Overall, this was an interesting first foray into computer vision, and we can see several ways in which this model can be refined for different uses. It could help to predict the emotions in a crowd by scanning security cameras, or be used as an aid in helping neurodivergent people train their brains to work with emotions. It could even be used as a way for actors to refine their emoting ability, by giving feedback on how well they express a target emotion. 

There are always ethical implications with machine learning, and that’s even more true with facial information, so any future uses or applications should always be considered thoughtfully and carefully before being implemented. For a longer exploration of this, please see Ian’s discussion on the implications of facial recognition in the final three slides of our Powerpoint presentation.
