# Automated Image Captioner
The idea of this program is to read an image and give a textual description of it. It uses concepts of NLP, CNN and RNN to process the information. This was designed using Python3 on Jupyter Notebooks.

## Steps to follow:
- In this project we have used Flickr 8k dataset for training and testing the model. Click [this link](https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_Dataset.zip) for downloading the dataset and [this link](https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_text.zip) for downloading the caption folder.
- Put these two folders along with this repo's jupyter notebook on the same folder.
- Now that you are ready with the setup, go to the jupyter notebook code and edit the path directories present in second cell.
- You are ready to go, run the cells serially, and the training begins at some point. The training takes fairly long time if you are using CPU.
- After that you can test with any image input, and observe the results.

## How the code works?

The code is fairly straightforward. First, we take Resnet (a convolutional neural network used to understand image input by converting it into a feature vector) to capture the feature vector of all the input image. This is important because, once the model understands the contents present inside the image, it'll be easy to map it with the caption text present.

Thus after we get the long vector containing features of all the images, we then do some preprocessing to the caption text. The words in the captions are converted to indices, which are vectorized to one hot encodings. After padding appropriately, we have a vector representing the texts, as well as a vector representing the input image features.

Now, we form a dual model, which runs parallelly, one for images and other captions. As we can see in the model description below, the first model takes encoded image vector as an input, and passes through dense layers followed by repeat vector; while the language model takes, the vectorized captions as input vector and passes through LSTM (a recurrent neural network which serves the purpose of understanding sentences and their meaning and context) and a time distribution which allows us to apply a layer to every temporal slice of an input.

<img src="https://user-images.githubusercontent.com/41820878/104118548-fc93d280-534f-11eb-90c7-cc6ac4e70987.png">

Finally after these 2 models are parallely processed they are now combined as shown above. The outputs from the image model and the language model is concatenated and passed through 2 LSTM networks followed by dense NNs. Finally a softmax activation is used giving a flattened output vector. Overall RMSprop is used as the optimizer.

During testing, the model looks at the objects and people present in the image and matches to the possible words and strings up a sentence. At times the sentence doesn't make complete sense, or has grammatical error. This is because some objects in the image might resemble to some other object during training leading to some misclassification. Or there were not enough sentences for the neural net to understand sentence formation thus leading to broken sentences. Overall the model well and captured quite relevant information.

## Some output screenshots
While the outputs from most of the images turned out to be good, some didnt make sense. As explained above in algo flow section, it is mainly because of over resemblance to some images and less number of captions.

<img src="https://user-images.githubusercontent.com/41820878/104119044-0834c880-5353-11eb-81ee-a330d5fb39e7.png">
<img src="https://user-images.githubusercontent.com/41820878/104119077-34504980-5353-11eb-98cd-472323f17c25.png">
<img src="https://user-images.githubusercontent.com/41820878/104119105-72e60400-5353-11eb-9a35-1e496371bb12.png">
<img src="https://user-images.githubusercontent.com/41820878/104119178-d112e700-5353-11eb-997f-faef6d10ac47.png">
<img src="https://user-images.githubusercontent.com/41820878/104119134-9741e080-5353-11eb-91ac-cc7af256a594.png">

## Contributions
Do not hesitate to contribute by [filling an issue](https://github.com/vat0599/Automated-Image-Captioner/issues) or [a PR](https://github.com/vat0599/Automated-Image-Captioner/pulls) !
