# tensorflow-image-classifier
Use Tensorflow to train and learn images

The original implementation can be found at 
https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/#0

We'll be using mobilenet with parameters 0.50 and 224 in this example.

# Folders layout:

- `photos`: contains all the photos for training the model
- `scripts`: will be calling the files here to run our model
- `tf_files`: outputs from the model
- `uploaded_photos`: dump photos that we want to classify into this folder.

# Opening Tensorboard

    tensorboard --logdir=tf_files/training_summaries &
    
# Training images

Run this to start training images:

    python -m scripts.retrain --bottleneck_dir=tf_files/bottlenecks --model_dir=tf_files/models/ --summaries=tf_files/training_summaries/mobilenet_0.50_224 --output_graph=tf_files/retrained_graph.pb --output_labels=tf_files/retrained_labels.txt --architecture=mobilenet_0.50_224 --image_dir=photos

This should take a little while.

# Classifying images

## Let's classify an iPhone 7 plus.

Let's use an annoymous photo of an iPhone 7 plus to validate our trained model:

    python -m scripts.label_image --graph=tf_files/retrained_graph.pb --image=uploaded_photos/photo1.jpg
    
You should get an output something like this:

    iphone 7 plus 0.989413
    xiaomi redmi 4a 0.00497179
    tulips 0.00374058
    roses 0.00186522
    sunflowers 5.5651e-06
    
## Let's classify a Xiaomi Redmi 4A 

    python -m scripts.label_image --graph=tf_files/retrained_graph.pb --image=uploaded_photos/photo2.jpg
    
You should get an output something like this:

    xiaomi redmi 4a 0.999836
    roses 7.8841e-05
    tulips 7.47027e-05
    iphone 7 plus 9.5819e-06
    dandelion 3.06468e-07




    