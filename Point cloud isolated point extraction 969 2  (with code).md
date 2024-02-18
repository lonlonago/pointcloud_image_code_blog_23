#  I. Introduction 

>  Previously, the function of past noise was used to eliminate high and low check point errors (point cloud to eliminate high and low errors), but the effect was not very good, so I thought about whether this kind of error could be eliminated by extracting isolated points. 

#  Second, algorithm implementation 

##  2.1 Implementation ideas 

>  Specific ideas: In point cloud data, if the number of points in a certain area of each point is less than a certain value, we can regard it as an isolated point. This is generally used to find isolated points in the air or below the ground. 

##  2.2 Implementation code 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574011270
 ```  
#  III. Achieving results 

>  Original data source 

![avatar]( 3adccf304b314ce8b94dc386cfdecc8d.png) 

>  After processing: 

![avatar]( 46306db41e304b339d0007f5490d492f.png) 

![avatar]( 26cbea819b754e8e96fea5e6c37a1131.png) 

![avatar]( 5a5062cb72a942fd8d254b142f075309.png) 

