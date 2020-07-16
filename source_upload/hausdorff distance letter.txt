import os
from PIL import Image
from itertools import combinations
import pandas as pd
import numpy as np
from scipy.spatial.distance import directed_hausdorff

# directed_hausdorff requires the location of point 

def get_points(bitmap):
    points = []
    for i in range(bitmap.shape[0]):
        for j in range(bitmap.shape[1]):
            if bitmap[i][j] == False:
                points.append((i,j))
    return points

### The function changes image files to 2d arrays and calculated the Hausdorff distancebetween those arrays ###
def hausdorff(file1,file2):
    x=Image.open(file1)
    x=x.convert('1')
    X=np.asarray(x)
    new_X = get_points(X)

    y=Image.open(file2)
    y=y.convert('1')
    Y=np.asarray(y)
    new_Y = get_points(Y)

    hd=max(directed_hausdorff(new_X, new_Y)[0], directed_hausdorff(new_Y, new_X)[0])
    return hd



