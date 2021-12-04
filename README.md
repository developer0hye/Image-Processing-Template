# Image-Processing-Template

## Image Processing

### Single Image Processing

```python
import cv2

path = ""
img =  cv2.imread(path)

# Processing
```

### Single-threaded Batch Image Processing

```python
import cv2
import numpy as np
import os
import tqdm

def read_files(root, ext=(".png", ".jpg", ".bmp", ".jpeg")):
    files_path = []
    for r, d, f in os.walk(root):
        for file in f:
            if file.lower().endswith(ext):
                file_path = os.path.join(r, file).replace(os.sep, '/')
                if not os.path.isfile(file_path):
                    continue
                files_path.append(file_path)
    return files_path

if __name__ == "__main__":
    files = read_files("path")
    for file in tqdm.tqdm(files):
        img = cv2.imread(file)

        #Processing
```


### Multithreaded Batch Image Processing

```python

```


## Utils

### Read an Image from Path with Unicode 
```python
import cv2
import numpy as np

def imread(file):
    img = np.fromfile(file, np.uint8)
    img = cv2.imdecode(img, cv2.IMREAD_COLOR)
    return img
```

### Write an Image to Path with Unicode

```python
import os
import cv2

def imwrite(filename, img, params=None): 
    try: 
        ext = os.path.splitext(filename)[1] 
        result, n = cv2.imencode(ext, img, params)
        if result: 
            with open(filename, mode='w+b') as f:
                n.tofile(f) 
            return True 
        else: 
            return False
    except Exception as e:
        print(e) 
        return False
```
