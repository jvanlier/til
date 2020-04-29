OpenCV2 Color Order, BGR v.s. RGB
=================================

OpenCV uses BGR (Blue, Green, Red) while matplotlib uses RGB.
To read with cv2 and display with matplotlib, the order needs to be swapped.

I have been doing nasty numpy array indexing to change the order, and even wrote functions like this in the past:

```python
def cv_to_mpl(cv_img):
    b, g, r = cv2.split(cv_img)
    return cv2.merge((r, g, b))
```

However, a more straightforward way is to just use the built-in `cv2.cvtColor` function with flag `cv2.COLOR_BGR2RGB` (or `cv2.COLOR_RGB2BGR` for the inverse transform):

```python
img_bgr = cv2.imread("some_image.jpg")
img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
```

(This can, of course, still be wrapped into a `cv_to_mpl` function to hide the details of the ordering).
