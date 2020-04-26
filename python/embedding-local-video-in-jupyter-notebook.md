# Embedding Local Video in Jupyter Notebook

Showing a video that was just created with Python code in a Notebook, with timeline and controls, is as simple as:

```python
from IPython.display import HTML
path_to_video = "videos/my_video.mp4"

HTML("""
<video width="960" height="540" controls>
  <source src="{0}">
</video>
""".format(path_to_video))
```

Thanks to the HTML5 Video tag.

