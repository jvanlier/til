# Deep Learning with Keras: Normalization for Pre-Trained Networks

Keras has a couple of pre-trained networks that can be used for transfer learning. They're also called "applications". Not all network use the same normalization method, and choosing the one method can cause transfer learning to not work (well).

Here's how to figure out how to normalize your data, depending on the chosen network.

## Step 1: find your network
Take a look here: https://github.com/keras-team/keras-applications/tree/master/keras_applications and find the network you're using. I'm going with MobileNet V2.

Find the `preprocess_input` function. MobileNet V2 defers to `imagenet_utils` with mode `tf`: https://github.com/keras-team/keras-applications/blob/bc89834ed36935ab4a4994446e34ff81c0d8e1b7/keras_applications/mobilenet_v2.py#L108

## Step 2: check `imagenet_utils`
As can be seen here, the normalization is `x /= 127.5; x -= 1`: https://github.com/keras-team/keras-applications/blob/master/keras_applications/imagenet_utils.py#L42-L45

If you repeat the same check for ResNet 50, you'll see that they only do mean subtraction (with means from ImageNet training data). That's a pretty big difference!

