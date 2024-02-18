#  I. Introduction 

>  Bounding box is an algorithm for solving the optimal bounding space of discrete point sets. The basic idea is to replace complex geometric objects approximately with geometric bodies (called bounding boxes) that are slightly larger in size and have simple characteristics. (From Baidu) The commonly used algorithms for solving bounding boxes mainly include AABB and OOB algorithms, but the AABB algorithm is easily affected by the orientation of objects, resulting in large gaps. Therefore, this paper will use the idea of OOB algorithm to achieve the minimum bounding box. There are many applications of bounding boxes, such as mechanical collision testing, object recognition and positioning, etc. Many scholars have used them in various fields. 

#  Second, algorithm implementation 

##  2.1 Algorithm steps 

>  1. First de-averaging and constructing the covariance matrix of the point cloud data, using the principal component analysis method to obtain the three principal axis directions (eigenvectors) of the data to construct a new feature space 

          O 

         \Omega 

     Omega. 2. Project the original data source to 

          O 

         \Omega 

     In Ω space, and obtain the maximum and minimum points of the projection data in the three axes. 3. In 

          O 

         \Omega 

     Omega space, to obtain the most value of the six points to construct the bounding box, and then the bounding box coordinates are re-projected to the original coordinate system to obtain the original data source along the main direction of the minimum bounding box. 

##  2.2 Code implementation (MATLAB) 

>   MinimumEnclosingCubeV3 .m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574053550
 ```  
#  III. Achieving results 

![avatar]( 70ea3b03896549a4a0f12510b3cd1811.png) 

![avatar]( 7a89120633fb4d76acc4b1a83917c414.png) 

![avatar]( 645aea65f6f04e0abd5cb2900da2c25c.png) 

![avatar]( 7792db2aa7394e79af04edf9cddd6f26.png) 

