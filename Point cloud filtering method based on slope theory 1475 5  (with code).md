#  I. Introduction 

>  Basic principle: Generally, we believe that the terrain surface is smooth and smooth, and the possibility of sudden changes in the terrain in the local area is small. By comparing whether the high difference between two points satisfies the height difference function, we can determine whether the point is a ground point. 

>  The method considers that the terrain surface is a gentle and smooth curved surface, and the possibility of sharp changes in the terrain in the local area is small. That is, when the height difference between adjacent two points exceeds a certain threshold, the smaller the distance between the two points, the smaller the probability that the point with a large elevation value belongs to the ground point. The height difference function is a filtering function based on the height difference and distance values between the two points, as follows: 

![avatar]( 92831e8b4c134d038030929afa26b5c5.png) 

>  The S * d in the filter kernel formula is actually to calculate the maximum allowable height difference between the two points. The following part adds a confidence interval according to the meaning of the paper, so that 5% of the noise points can be allowed. 

#  Code implementation 

The results here are not ideal, and improvements need to be made in the future. Let's record it here first. 

>  Slope.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574011948
 ```  
#  III. Achieving results 

>  primordial point cloud 

![avatar]( 13e2cc7ae7e5452c97991b3b9b0c1e69.png) 

>  Result image 

![avatar]( 4a9da99c730646809c793a2d4f7bd384.png) 

![avatar]( 98fca49510a44cf8b994755754077f8c.png) 

#  IV. Summary 

>  From the results, the point cloud filtering based on the slope theory is very similar to the layer algorithm in CloudCompare, and the processing results all contain some floating objects. In addition, the slope algorithm needs to calculate the height difference for each point, so the computational efficiency needs to be improved. Many papers have proposed improved methods. Interested students can find some literature for in-depth research. 

>  References: [1] Slope-based filtering of laser altimetry data [2] Urban LiDAR point cloud filtering method based on slope and regional growth 

