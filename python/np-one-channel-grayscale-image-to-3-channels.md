numpy one channel (grayscale) image to 3 channels
=================

When working with images, you might have a one channel (grayscale) image with some highlighted pixels (e.g. edge detection, color thresholding). 
I'm assuming below that pixel values range from 0 to 1.

While it normally suffices to visualize these things like this:

```python
plt.imshow(binary_img, cmap="gray")
```

It may sometimes be needed to replicate the pixel values across the 3 channels, e.g. to include them in a side-by-side image or video with the original.
That can be done easily with numpy as follows:

```python
img = np.repeat((binary_img * 255)[:, :, np.newaxis], 3, axis=2)
```

Couple pointers:
- The `* 255` is included because of the asumption that pixel values are from 0 to 1. Change accordingly if they aren't.
- Might need to replace `binary_img` with `binary_img.astype(np.uint8)` if it isn't that dtype already.
