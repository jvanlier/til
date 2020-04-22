CV2 Region Of Interest `fillPoly`
===============

Creating a Region of Interest Polygon and mask out everything else.

I've already done this many times before, yet I end up looking it up in old code more often than I'd like. Here's one version that works on RGB images with 3 channels and on gray scale images with just 1 channel.

```python
def apply_roi(image, roi):
    stencil = np.zeros(image.shape).astype(image.dtype)
    n_channels = 1 if len(image.shape) < 3 else image.shape[2]
    cv2.fillPoly(stencil, roi, [255] * n_channels)
    return cv2.bitwise_and(image, stencil)
```

Arg `roi` is a 2d numpy array with integers, for example: `np.array([[(100, 540), (470, 310), (480, 310), (910, 540)]], dtype=np.int32)`.
