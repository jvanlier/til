Modify Video Frames Easily with MoviePy
=============

MoviePy enables modifying videos frame-by-frame using only 3 lines of code (excluding the import and the actual modification):

```python
from moviepy.editor import VideoFileClip

clip = VideoFileClip("input_video.mp4")
new_clip = clip.fl_image(process_image)
new_clip.write_videofile("output_video.mp4", audio=False)
```

Where function `process_image` has a straight forward signature: `process_image(image: np.ndarray) -> np.ndarray`.
