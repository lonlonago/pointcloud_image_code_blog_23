#  I. Introduction 

>  The essence of point cloud plane fitting is to replace the point cloud that is approximately located in the same plane with a fitting plane, so that the sum of the squares of the distances from all points in the point cloud to the fitting plane is minimized, and the height of the point cloud and the fitting plane is consistent. There are many existing methods, such as least squares method, eigenvalue method, etc. This paper will use least squares method to realize simple plane fitting. 

>  Among them, there are two ways of programming the least squares method: (1) by using the covariance matrix (symmetric matrix) to solve; (2) by using the partial derivative method to solve, the details can be read in the literature [1]. The final result of these two methods is essentially the same. Here we use the method in (1) to realize the fitting process, assuming that the plane equation is: 

>  If the point set is 

           p 

           1 

          , 

           p 

           2 

          . 

          . 

          . 

           p 

           n 

         p_1,p_2...p_n 

     P1, p2... pn, then the equation becomes: 

>  Set: 

>  The original formula can be changed to: 

#  Second, algorithm implementation 

>  main.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574068532
 ```  
>  DarwPlane.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574068532
 ```  
#  III. Achieving results 

![avatar]( a1514a9e8515421d8e165a2f89d037f4.png) 

![avatar]( 38c69e91cf464f9490c2fb5c74815079.png) 

#  References 

>  [1] An improved least squares plane fitting algorithm 

