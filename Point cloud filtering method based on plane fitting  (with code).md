#  I. Introduction 

>  In urban and suburban areas with little change in topography, the topography of these areas can be regarded as a continuously distributed curved surface. Then in a small area, the curved surface can be approximated as a plane. The plane fitting method is to use ground points to fit a plane in a local area, and determine whether other points belong to the plane through certain criteria. 

#  Second, algorithm implementation 

##  2.1 Implementation steps 

>  Step1: Use a large moving window to search for the lowest point in the window, and fit the plane equation of the ground (ground model) from the whole of the lowest point found in each moving window. Step2: Compare all points with the ground model, calculate the distance (height difference) from each point to the plane, where the height difference exceeds a certain threshold, it is considered a non-ground point, and filter out these points; Step3: Reduce the window, calculate the ground model for the remaining ground points according to steps 1 and 2, change the threshold, and further filter out the points with a large height difference with the current ground model. After repeating several times, a more accurate set of ground points is obtained. 

##  2.2 Implementation code 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574024455
 ```  
#  III. Achieving results 

![avatar]( 14c96945fc6143ab8d45ca14b522e7ab.png) 

![avatar]( 7e5a284563eb4d18896757ce00d2b402.png) 

![avatar]( f13d07283d234d2cb65dbb8a5c2e0941.png) 

#  References 

>  [1] A LIDAR point cloud filtering method based on plane fitting 

