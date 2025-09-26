The main idea finding the flag using OpenCV library and Python.

1. After we download `confetti.zip`, we see that we have 500 photos. Each dimension is 500 × 1 and according to problem statement, the image size is 500 × 500.
2. So basically, we have to concatenate the 500 images in **vertical** fashion.
3. Make a directory to extract all 500 images and set your `pwd` to that directory containing all images. After that only work is to join all images.
4. I executed this simple `Concatenate.py` script and it worked.
```python
from PIL import Image

listimages=[]
for i in range(0,500):
    listimages.append(Image.open(str(i) + ".png"))  # Make a list of pointers to the 500 pictures.

concatenate=Image.new("RGB",(500,500))              # Size of the concatenate picture
Y_offset=0

for i in listimages:
    concatenate.paste(i,(0,Y_offset))
    Y_offset+=1                                     # Add 1 at a time , Because the height of each picture is 1.
concatenate.save("concatenate.png")
```

We get the output as `concatenate.png` after the above script is run. The image is as follows:
![[the_adventure_of_boris.png]]

We see a hex code in between.

7. The Hex code is as follows: `66 6c 61 67 7b 74 68 33 5f 4b 47 42 5f 6c 30 76 33 73 5f 43 54 46 7d` I converted it to text online to get the flag.

Flag: ``flag{th3_KGB_l0v3s_CTF}``

