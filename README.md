# My Basic-Computer-Vision
<hr>

## Library used
<ul>
  
### OpenCV: Open Source Computer Vision Library 
github OpenCV : <https://github.com/opencv/opencv>

#### Resources

* Homepage: <https://opencv.org>
  * Courses: <https://opencv.org/courses>
* Docs: <https://docs.opencv.org/master/>
* Q&A forum: <https://forum.opencv.org>
  * previous forum (read only): <http://answers.opencv.org>
* Issue tracking: <https://github.com/opencv/opencv/issues>
* Additional OpenCV functionality: <https://github.com/opencv/opencv_contrib> 


#### Contributing

Please read the [contribution guidelines](https://github.com/opencv/opencv/wiki/How_to_contribute) before starting work on a pull request.

##### Summary of the guidelines:

* One pull request per issue;
* Choose the right base branch;
* Include tests and documentation;
* Clean up "oops" commits before submitting;
* Follow the [coding style guide](https://github.com/opencv/opencv/wiki/Coding_Style_Guide).
<br>
</ul>
<hr>
  
## Source code and result

- <h4>goto file</h4>
<a href = "https://github.com/boss2546th/Basic-Computer-Vision/blob/main/pythonProject3/imread.py">
  <img src = "https://user-images.githubusercontent.com/61747927/143782748-b06790c1-b42c-4496-acb4-34e3d5d691cc.png" width = 150px>
</a> 
<br>
<br>
  
 ```python
import cv2
import numpy as np
import time as tm
```
```python
img = cv2.imread('243922751_1753233418210283_3024483077450698404_n.jpg')
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

lower = np.array([0, 150, 150])
upper = np.array([75, 255, 255])
result = cv2.inRange(hsv, lower, upper)
res = cv2.bitwise_and(img, img, mask= result)
  

```python
def resize(img,per):
    scale_percent = per  # percent of original size
    width = int(img.shape[1] * scale_percent / 100)
    height = int(img.shape[0] * scale_percent / 100)
    dim = (width, height)
    # resize image
    return cv2.resize(img, dim, interpolation=cv2.INTER_AREA)
```
```python
X = int(742/12)
Y = int(470/9)
cnt = 0

ssrc = []
ssrcE = []
for i in range(1, 10):
    k = ((i%2)-1)
    yy = (Y*i)+ 10
    yx = yy-Y
    for j in range(1, 13+k):
        if i%2 != 0:
            xy = X*j
            xx = xy - X
            cv2.line(result, (xy, yx-10), (xy, yy-10), (255, 255, 255), 1)
        elif i%2 == 0:
            xy = (X * j) + 35
            xx = xy - X
            cv2.line(result, (xy, yx-10), (xy, yy-10), (255, 255, 255), 1)
        ssrc.append(resize(result[yx+7:yy-7 , xx+7:xy-7],350))
        ssrcE.append(result[yx + 7:yy - 7, xx + 7:xy - 7])
        #cv2.imshow('Block', result[xx:xy, yx:yy])
        #tm.sleep(0.5)


for i in range(1,10):
    cv2.line(result, (0, Y*i), (742,Y*i), (255, 255, 255), 1)
print(len(ssrc))
for i in range(len(ssrc)):
    contours, hierachy = cv2.findContours(ssrc[i], cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    allcon = [len(ii) for ii in contours]
    try:
        mxa = max(allcon)
    except:
        mxa = 0
    cv2.putText(ssrcE[i], str(mxa), (2, 15), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (90, 0, 0), 2, cv2.LINE_AA)
    #cv2.imshow(str(i+1), ssrc[i])
    cnt = (cnt + 1) if mxa > 30 else cnt
    opt = " True!! : " if mxa > 30 else " false : "
    print("Max Contours found ="  + opt + str(mxa))

print("Number of vegetable found = " + str(cnt))

lst = [img,res,result]
lstend = [resize(i,75) for i in lst]
result = resize(cv2.inRange(hsv, lower, upper),75)
cv2.imshow('img',lstend[0])
cv2.imshow('res',lstend[1])
cv2.imshow('result_mini',lstend[2])
cv2.imshow('result',result)
print("Accuracy is %.2f" %((cnt/35)*100) + " % (count by human = 35)")
print(img.shape[1],img.shape[0])

cv2.waitKey(-1)
cv2.destroyAllWindows()
 ```
 
<br>

![Screenshot 2021-10-04 141212](https://user-images.githubusercontent.com/61747927/142733487-8cdbfd08-7d52-42ca-92a9-cd356541dfd5.jpg)<br>
![Screenshot 2021-10-04 135814](https://user-images.githubusercontent.com/61747927/143809909-6336e377-ebd5-47c0-be1e-f0af7c0a7a6c.jpg)

  <hr>
