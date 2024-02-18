#  Overview of the principle 

>  Basic principle: The spatial relationship of the laser point cloud reflects the spatial changes of the terrain surface. For any complex spatial surface, its local surface elements can be fitted using a simple quadric surface. 

>  The specific calculation process: (1) point cloud grid, select the lowest point of the grid in a certain size window to construct a quadric surface (here we use the least squares method to fit the quadric surface, the specific content can refer to the point cloud least squares method to fit the quadric surface); (2) Compare the distance from the point cloud to the fitted surface in the calculation window with the set height difference threshold. If it is smaller than this threshold, it is classified as a ground point; otherwise, it is classified as a non-ground point. This method is suitable for terrain areas with certain terrain undulations but not very steep. 

#  Implementation code 

>  SurfaceFit.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574043294
 ```  
#  III. Achieving results 

![avatar]( e410b931cd154d278412278d0854288d.png) 

![avatar]( 42f2cc023bde400a9343edb4a3b2a1bc.png) 

