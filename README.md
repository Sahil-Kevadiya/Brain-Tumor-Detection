# Brain-Tumor-Detection<h1>Data Augmentation:</h1>
Why did I use data augmentation?

Since this is a small dataset, There wasn't enough examples to train the neural network. Also, data augmentation was useful in taclking the data imbalance issue in the data.

Further explanations are found in the Data Augmentation notebook.

Before data augmentation, the dataset consisted of:
155 positive and 98 negative examples, resulting in 253 example images.

After data augmentation, now the dataset consists of:
1085 positive and 980 examples, resulting in 2065 example images.

Note: these 2065 examples contains also the 253 original images. They are found in folder named 'augmented data'.

<h1>Data Preprocessing</h1>
For every image, the following preprocessing steps were applied:

Crop the part of the image that contains only the brain (which is the most important part of the image).
Resize the image to have a shape of (240, 240, 3)=(image_width, image_height, number of channels): because images in the dataset come in different sizes. So, all images should have the same shape to feed it as an input to the neural network.
Apply normalization: to scale pixel values to the range 0-1.
Data Split:
The data was split in the following way:

70% of the data for training.
15% of the data for validation.
15% of the data for testing.
Neural Network Architecture

<h1>Neural Network Architecture</h1>

Understanding the architecture:
Each input x (image) has a shape of (240, 240, 3) and is fed into the neural network. And, it goes through the following layers:

A Zero Padding layer with a pool size of (2, 2).
A convolutional layer with 32 filters, with a filter size of (7, 7) and a stride equal to 1.
A batch normalization layer to normalize pixel values to speed up computation.
A ReLU activation layer.
A Max Pooling layer with f=4 and s=4.
A Max Pooling layer with f=4 and s=4, same as before.
A flatten layer in order to flatten the 3-dimensional matrix into a one-dimensional vector.
A Dense (output unit) fully connected layer with one neuron with a sigmoid activation (since this is a binary classification task).
Why this architecture?

Firstly, I applied transfer learning using a ResNet50 and vgg-16, but these models were too complex to the data size and were overfitting. Of course, you may get good results applying transfer learning with these models using data augmentation. But, I'm using training on a computer with 6th generation Intel i7 CPU and 8 GB memory. So, I had to take into consideration computational complexity and memory limitations.

So why not try a simpler architecture and train it from scratch. And it worked :)

<h1>Training the model</h1>
The model was trained for 24 epochs and these are the loss & accuracy plots:

Loss plot

![image](https://github.com/Sahil-Kevadiya/Brain-Tumor-Detection/assets/138906113/e4f30482-5be7-4861-8f09-6e5ed1fbfb9d)

Accuracy plot

![image](https://github.com/Sahil-Kevadiya/Brain-Tumor-Detection/assets/138906113/9914a78b-e683-48c0-a777-9550c00e5be7)


The best validation accuracy was achieved on the 23rd iteration.
