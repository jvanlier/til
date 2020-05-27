Matpotlib Plot Many Images
==========================

Convenient function for plotting many images in subplots.

This isn't something I learned today, but I am finding myself constantly reproducing variants of this function. Hence, I figured let's create a nice version, with DocString and type hints, that can be easily copied to notebooks and adjusted as required.

This function can be easily extended to show additional information, e.g. model predictions using `ax.title(...`), or
saved with `plt.savefig(...)`, etc. Note that I'm assuming that all images have the same dimensions (hence `sharex` and `sharey`), remove if not the case.

```python
from typing import Union, Collection
from math import ceil
from itertools import zip_longest
from pathlib import Path

import matplotlib.pyplot as plt


def plot_many_images(img_paths: Collection[Union[str, Path]], 
                     suptitle: str = None,
                     ncols: int = 6,
                     figsize_x: int = 18, 
                     figsize_y_per_row: int = 4):
    """Plot many images using subplots.
    Automatically determines appropriate number of rows and turns off axes when a row can't be 
    filled completely.
    Automatically adjusts tight_layout rect if suptitle is provided.
    
    Args:
        img_paths: Collection (e.g. List/Array) of Path instances or plain old strings 
            with path of images to plot.
	suptitle: Title on top.
        ncols: number of columns
        figsize_x: the width of the image
        figsize_y_per_row: the height of the image *per row*. Usually requires some tweaking 
            depending on image size.
    """
    nrows = ceil(len(img_paths) / ncols)
    
    _, axes = plt.subplots(nrows=nrows, ncols=ncols, 
                           figsize=(figsize_x, nrows * figsize_y_per_row), 
                           sharex=True, sharey=True)
    
    for img_path, ax in zip_longest(img_paths, axes.ravel()):
        if not img_path:
            ax.axis("off")
            continue
            
        img = plt.imread(str(img_path))
        ax.imshow(img)
        
    if suptitle:
        plt.suptitle(suptitle)
        # Tight layout doesn't take into account suptitle, make a bit more room in the top:
        plt.tight_layout(rect=[0, 0, 1, 0.96]) 
    else:
        plt.tight_layout()

    plt.show()
```
