>  Because I am also very interested in filtering, I found a literature to reproduce its algorithm. I feel that the effect is not bad, so I specially recorded it. 

![avatar]( 244315625d304ce0a879b3a152cb1f8f.png) 

![avatar]( e4479b742e1f491193a51accb2c395ae.png) 

#  I. Introduction 

>  The point cloud filtering method based on regional growth is a typical method that considers the structural characteristics in the local range. In essence, it is still based on the sudden elevation to achieve the filtering effect, so it still requires us to set the height difference threshold. For details, you can read the algorithm steps and code below to understand. 

#  Second, algorithm implementation 

##  2.1 Implementation steps 

>  1. Divide the point cloud blocks. What are the benefits of dividing the point cloud into pieces in this way? The main advantage is that it can avoid the situation of using a single seed point to obtain all the ground points of the entire terrain. To be honest, this is also unrealistic, because it is very difficult to filter due to the undulating terrain. The specific division is actually very simple. First, use prior knowledge to evaluate the topography of the survey area. Under the premise of ensuring that the terrain changes of each Block have a certain uniformity, the survey area is divided into regular rectangles. The size of the rectangle depends on the maximum building size in the survey area (to prevent the top of the building as a ground point). It is necessary to ensure that each point cloud block rectangle contains ground points, which is convenient for us to set up subsequent seed points. 2. Grid the point cloud blocks. For each Block, in order to facilitate the search and judgment of seed points, the original discrete point cloud data is regularly gridded on the horizontal plane. I have been unable to understand the grid before, but now it is much better, because if you use kdtree or octree, their time complexity is O (logn), but if you grid, the complexity of finding the adjacent points of a point is only O (1). 3. Select the initial seed point. Select the ground point with the lowest elevation in the point cloud block area as the initial seed point. 4. Grow. Perform an 8-neighborhood search centered on the initial seed point to determine whether the height difference between the pending point and the known seed point meets the threshold. If so, the pending point is a ground point, otherwise, the point is a ground feature point (new seed point). I only used the slope theory for the height difference setting here 

          h 

          = 

          S 

          ∗ 

          d 

         h=S*d 

     In this part, no confidence interval is set (if you don't know much about slope theory, you can see this article: point cloud filtering method based on slope theory), because you want to see the effect first "~". 5. Repeat the process of 3 and 4 until there are no points that meet the conditions. 

##  2.2 Implementation code 

>  The code is a preliminary implementation of regional growth filtering. In fact, there are many improvement strategies, such as eliminating side information, which I have not adopted here. I need to read and study more deeply in the future. 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957408081
 ```  
#  III. Achieving results 

>  Here I found an example data in PCL to test (parameter settings: dx = 10, dy = 10; bx = 3, by = 3) 

![avatar]( 6c013591f53441a1bc8eb560ab58777b.png) 

![avatar]( 7b76e52855d644d1b9a9df0a23199d5b.png) 

>  I found a previous example data to test (parameter settings: dx = 0.3, dy = 0.3; bx = 0.1, by = 0.1) 

![avatar]( e8c5741c20884624845dd190e30b3b1c.png) 

![avatar]( f5f137a337c64d8fb596a4dde7633e73.png) 

#  References 

>  [1] LIDAR point cloud data filtering based on regional growth [2] Urban LiDAR point cloud filtering method based on slope and regional growth [3] Airborne laser data filtering method based on distance limitation 

