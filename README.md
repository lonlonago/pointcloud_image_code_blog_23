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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  I. Introduction 

![avatar]( 5a62d26348324db29a3d37e59515d159.png) 

>  Among them, the third step uses the least squares method to estimate the specific process of principal curvature, as follows: 

![avatar]( 0781d911d3fe47ac99e5a3c44b7acba2.png) 

 ![avatar]( 302576da0a0c46fe845ccf8186773551.png) 

#  Code implementation 

>  GaussCurvature.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574071059
 ```  
#  III. Achieving results 

![avatar]( 2381bbedf7cf4a36b7e705c2d45a9389.png) 

#  reference 

>  [1]一种基于高斯曲率的ICP改进算法 [2]Robust Curvature Estimation and Geometry Analysis of 3D point Cloud Surfaces [3]Curvature Estimation of 3D Point Cloud Surfaces Through the Fitting of Normal Section Curvatures 



--------------------------------------------------------------------------------

#  I. Introduction 

>  I accidentally saw such a point cloud hole patching method before, and I felt very interesting. I downloaded the author's source code to see the effect. The specific process is as follows: 1. First, we need to locate the holes on the grid first. 2. Then calculate the center position of the vertices on the hole boundary (the average of the vertex positions on the hole boundary). The vertices on the boundary are connected to the newly created vertices at the center position, thus creating a surface patch that fills the holes. The triangles in this patch will be upsampled (subdivided), so that when we perform patch smoothing, we can have more vertices to operate on. 

Note that the triangle of the original mesh is upsampled here, as this makes it very easy to fuse the vertices of the original patch and the original geometric shape together. "Fusion" means ensuring that the boundaries of the original mesh and the boundaries of the patch share the same vertices. 

>  3. Next, by solving the equation on the patch 

           W 

           2 

          f 

         D ^ {2} f 

     Delta 2f = 0 to create a smooth patch. This requires a discrete Laplace operator to achieve this, and the dispersion of a Laplace operator on the surface of the grid is called a Laplace-beltrami operator. Here a discrete Laplace-beltrami operator is created using the libigl library and then used to solve the equation 

           W 

           2 

          f 

         D ^ {2} f 

     D2f = 0. 

>  4. Finally, we use the mesh extraction algorithm to downsample the mesh to obtain the final patched result. 

More details can be found: https://erkaman.github.io/posts/hole_filling.html. 

#  Implementation code 

>  CMakeLists.txt 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 20240203095740806
 ```  
Here are some changes to the original code to make it more in line with my habits. 

>  main.cpp 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 20240203095740806
 ```  
All the code can be clicked on the URL: https://github.com/Erkaman/hole_fixer. 

#  III. Configuration work 

>  1. After the code is obtained, first use the cmake tool to generate the VS project. 

![avatar]( 0270d62653a1a6f1e2e840ae4ffbaa6c.png) 

>  2. Right-click "ALL BUILD" to generate all projects. After generating all projects, set the corresponding command line parameters. 

![avatar]( 8e4596b986505a234079ee0f3a2a2f0b.png) 

![avatar]( 00a61862f7c6f1a7f94c4cbacda7d2c5.png) 

>  3, finally set hole_fixer project to start the project, run the program on it. 

![avatar]( 81a061a8a65ad5044514e848a44c5200.png) 

#  IV. Implementation effectiveness 

![avatar]( c4599578772cc481cfc8293bbd1701da.png) 

![avatar]( d7de2d660959af5ae00c334401e5df39.png) 

However, it can be clearly seen that the effect of the repair is not very ideal. The patch part is obviously very different from the surrounding mesh density, which requires subsequent shaping. 

#  IV. References 

>  [1]https://github.com/Erkaman/hole_fixer 



--------------------------------------------------------------------------------

#  I. Introduction 

>  STL file format is a model file format created by 3D Systems, which is used to represent triangular meshes, mainly used in CAD and CAM fields. STL can only be used to represent closed surfaces or volumes functionally, and there are two file formats: text and binary. 

>  The first line of the STL file gives the file path and file name, and the following line gives the geometric information of the triangular facets, each line starting with 1 or 2 keywords. The STL file format organizes data in units of triangular facets, and each triangular facet consists of 7 lines of data: facet normal is the normal vector coordinate of the triangular facet pointing to the outside of the entity, outer loop description The following 3 lines of data are the 3 vertex coordinates of the triangular facet, and the 3 vertices are arranged counterclockwise in the direction of the normal vector pointing to the outside of the entity. The last line is the end flag. As shown in the figure below: 

![avatar]( b1bd6d09e3d844f3a2d10bb5c6fe0689.png) 

#  II. Document reading and writing 

Here we use the official provided stlwrite.m and stlread.m two function files, but the official download network speed is a bit slow, you can download through this link: https://download.csdn.net/download/dayuhaitang1/85036426. The following shows how to use these two files: 

>  ReadStl.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574059477
 ```  
>  WriteStl.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574059477
 ```  
#  Third, read and write effects 

>  Original data source 

![avatar]( 88fb19d512c84651ac3283ac367c427d.png) 

>  read 

![avatar]( 40e976d7e326418aad848b3ef20d10b5.png) 

>  Writing (taking convex and concave packets as examples) 

![avatar]( 0d94eca4a5124ce79b62beb203310a1d.png) 

![avatar]( 9cb61657759e4f0db6c19fbe1a4ffd5f.png) 



--------------------------------------------------------------------------------

#  I. Overview 

>  Among the many file formats for storing point clouds, some are "tailor-made" for point cloud data, and some file formats (such as computer graphics and 3D models in computer science or communication data files) have the ability to represent and store point clouds, and are applied to the storage of point cloud information. After years of development, the las file format has gradually become the industry standard format for LiDAR data. The format aims to provide an open format standard that allows different hardware and software providers to output interoperable unified formats. It is a binary file format. I've always wanted to use MATLAB to read and write LAS files. Although the point cloud toolbox in MATLAB can read LAS data, I didn't find out how to save it as LAS data. This is too much of a mess. I searched the Internet and found that other methods can be used. 

>  Here we will use some files written by a boss. I have put the file link at the end of the article, and students who need it can download it. 

>  The main functions used are export, and the parameters are as follows: 

![avatar]( 83ec3abbb098445dba322944631fcfb1.png) 

#  Implementation code 

>  lasIO.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574012502
 ```  
>  Some of the functions used above need to use the Point_cloud_tools_for_Matlab package, which is a boss wrote about some of the point cloud processing functions, including a variety of data format conversion, read and write, etc. GitHub download link: https://github.com/pglira/Point_cloud_tools_for_Matlab, if there are students too slow, I have uploaded to csdn, link: https://download.csdn.net/download/dayuhaitang1/85071981. 

#  III. Achieving results 

![avatar]( b42c8ff8f5444b1a98f1a986334832dc.png) 

![avatar]( b073707c16454ed7ad89e5a7501f96ea.png) 

![avatar]( df997159191e4149865b61dd9cef5d6e.png) 

>  The writing speed is much faster than that of pcwrite, and millions of points can be written in about 10 seconds. 

#  reference 

>  [1]https://www.geo.tuwien.ac.at/downloads/pg/pctools/pctools.html 



--------------------------------------------------------------------------------

#  I. Introduction 

>  XYZ and TXT files are the simplest storage formats for point cloud data. The first three columns are generally the XYZ location information of the point cloud, followed by fields such as color or normal vector. 

#  Second, file reading and writing code 

>  XYZReadWrite.h 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574026755
 ```  
>  main.cpp 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574026755
 ```  
#  III. Achieving results 

![avatar]( 25628ca024d2475a8ef41693c9a77b1a.png) 

![avatar]( d5ba56e917b84d6da4828d2071240d59.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

Because it is the teacher's homework, I recently studied the K-Means algorithm and took notes on it.  

#  First, the K-Means algorithm 

>  Among many clustering methods, the K-Means clustering method belongs to "prototype-based clustering" (also known as prototype clustering), which assumes that the clustering structure can be characterized by a set of prototypes and is very commonly used in real-world clustering. Usually, this type of algorithm will initialize the prototype first, and then iteratively update the prototype to solve it. Using different prototype representations and different solution methods will also produce different algorithms. 

As a classic "prototype clustering" algorithm, the prototype of the K-Means algorithm is "K cluster centers", and the iterative solution is based on the degree of change of the "centroid" (the average value of the x, y, and z coordinates of all points of the same class) solved by two adjacent solutions. This may also be the origin of the name of K-Means clustering: K cluster centers + centroid (coordinate average value). 

#  Second, K-Means algorithm steps 

The process is actually relatively simple: 

>  1. Initialize the prototype, that is, specify the K value and K cluster centers. The designation of cluster centers can be artificially entered, randomly selected, or in other ways, but try to ensure that the distance between cluster centers is not too close. 2. Clustering. Traverse all data points, calculate the distance from each data point to the K cluster centers (I choose the Euclidean distance here, or I can choose the Mahalanobis distance or other distances), and assign each data point to the category of the cluster center closest to the point until the last data point. 3. Update the cluster center. That is, calculate the centroid of each class, and compare the calculated cluster center with the previous cluster center. If all the cluster centers do not change, stop; if there is a change, the current cluster center is used as the new cluster center, and the above process of 2 and 3 is repeated until all the cluster centers do not change. 

#  Third, the code implementation effect 

Original data source: 

![avatar]( 20200501092319862.png) 

 The code is as follows: main.cpp: 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574072616
 ```  
Point3.h: 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574072616
 ```  
PointDataSource.h: 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574072616
 ```  
Kmeans.h: 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574072616
 ```  
Processing effect: 

![avatar]( 20200501093820797.png) 

 It can be seen from the processing renderings that the K-Means algorithm can cluster and identify ground objects with obvious differences in distance, but the algorithm will also cluster noise. So if the amount of data is large, then when using this method, simple denoising processing can be performed first, which can reduce the computational cost of the K-Means algorithm when clustering. 

>  Reference: "machine learning" 



--------------------------------------------------------------------------------

#  I. Introduction 

>  The approximate method of using the least squares method (point cloud least squares method to fit the plane) has been introduced before, and I will not go into details here. Here we use the same method to fit a curve, and the fitting equation is: 

#  Implementation code 

>  main.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574040318
 ```  
#  III. Achieving results 

![avatar]( 88f4a90a68ca4fd7af290f1a810b3ce2.png) 

>  The fitting effect here is not very ideal. It may be that the least squares method has received noise interference. Let's study it later. 

#  References 

>  [1] An automatic power line extraction method based on airborne LiDAR point cloud 



--------------------------------------------------------------------------------

#  Overview of the principle 

![avatar]( 68cc4b0136454f539dd2f34d5e05b8b4.png) 

#  Code implementation 

>  CircleFit.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574085755
 ```  
>  DrawCircle.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574085755
 ```  
#  III. Achieving results 

>  Original data source 

![avatar]( 891dfe7e810b4239a38ee635e7a693a6.png) 

>  fitting result 

![avatar]( 008868aaf23341e59c7e12c1ad3ebc56.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  I. Introduction 

>  Because the least squares method has been used many times before, for details, please refer to the article Point Cloud Least Squares Fitting Plane, which will not be described in detail here. For quadric surfaces, the general equation can be written as: 

>  among them 

          x 

          , 

          y 

         x,y 

     X and y are all known numbers, so this form of equation is easy to solve for the correlation coefficients using the least squares method. For details, please refer to the code below. 

#  Code implementation 

>  surface.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574029626
 ```  
>  DrawSurface.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574029626
 ```  
#  III. Achieving results 

![avatar]( db65885ebbe74952ba227b18340530f1.png) 

![avatar]( 78fe436e9986461a99134761b8c4a0fc.png) 



--------------------------------------------------------------------------------

#  Overview of the principle 

>  A straight line in three dimensions, unlike a straight line in two dimensions, cannot be written 

          a 

          x 

          + 

          b 

          y 

          + 

          c 

          z 

          + 

          d 

          = 

          0 

         ax+by+cz+d=0 

     The form of ax + by + cz + d = 0, because this is a plane expression in three-dimensional space, then the line expression in three-dimensional space is generally the simultaneous of two planes, but this is also relatively complicated. Here we use the expression of the point-oriented line to carry out the line fitting process. 

>  Point equation:  

             x 

             − 

              x 

              0 

            a 

           = 

             y 

             − 

              y 

              0 

            b 

           = 

             z 

             − 

              z 

              0 

            c 

          \frac{x-x_0}{a}=\frac{y-y_0}{b}=\frac{z-z_0}{c} 

      ax−x0​​=by−y0​​=cz−z0​​ 其中， 

          v 

          = 

          （ 

          a 

          , 

          b 

          , 

          c 

          ） 

         v=（a,b,c） 

     V = (a, b, c) is the direction vector, ( 

           p 

           0 

          = 

           x 

           0 

          , 

           y 

           0 

          , 

           z 

           0 

         p_0=x_0,y_0,z_0 

     P0 = x0, y0, z0) is a point on a straight line. The vectors here are all column vectors by default. 

>  Next, let's find the distance from a point to this straight line. 

![avatar]( 7e323abe9125498cad82cf1d8e431099.png) 

>  As shown in the figure above, you only need to use vectors 

           p 

           0 

           p 

           1 

          ( 

           Y 

           1 

          ) 

         p_0p_1(Y_1) 

     The Modular Square of p0 p1 (Y1) and the Projection on a Straight Line 

           q 

           1 

          ( 

          ( 

           Y 

           1 

           T 

          ∗ 

          v 

          ) 

          ∗ 

          v 

          ， 

          ∥ 

          v 

          ∥ 

          = 

          1 

          ) 

         q_1((Y_1^T*v)*v，\lVert v\rVert = 1) 

     The difference between the modulo square of q1 ((Y1T * v) * v, < unk > v < unk > = 1) can be found 

          D 

         D 

     D squared, then we can get the target equation: 

>  Our goal is to make 

          f 

         f 

     F is the smallest, right? 

          Y 

         Y 

     Take the partial derivative of Y and make it equal to 0. 

>  At this point we can get 

          ∑ 

           Y 

           i 

          = 

          0 

         \sum{Y_i}=0 

     Yi = 0, from this 

           p 

           0 

          = 

            ∑ 

             Y 

             i 

           n 

         p_0=\fracsum{Y_i}}{n} 

     P0 = n < unk > Yi, it is surprising to find that using the least squares method to fit a straight line must pass through the center (centroid) of all points. 

>  But it's also true. 

          v 

         v 

     The partial derivative of v cannot be found 

          v 

         v 

     The value of v, due to the special property of the direction vector 

           v 

           T 

          v 

          = 

          1 

         v^Tv=1 

     vTv = 1, but it can be substituted into the original formula (for the specific derivation process, please refer to the http://www.whudj.cn/?p=72 of this article), that is, it can be changed into the following formula: 

>  Ultimately, it can be reduced to the following form: 

>  We want to make 

           v 

           T 

          S 

          v 

          = 

          0 

         v^TSv=0 

     vTSv = 0, then just find 

          S 

         S 

     The eigenvector corresponding to the smallest eigenvalue of S is enough, that is 

           Y 

           i 

           Y 

           i 

           T 

         Y_iY_i^T 

     Yi YiT matrix corresponding to the maximum eigenvalue of the vector. 

#  Code implementation 

>  LineFit.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574087376
 ```  
#  III. Achieving results 

![avatar]( 536d6d53874841cb9575648b97d4ec6f.png) 

#  reference 

[1]http://www.whudj.cn/?p=72 



--------------------------------------------------------------------------------

#  I. Introduction 

>  Here we will no longer carry out the derivation process of the formula, because in the previous article, the point cloud least squares fitting space straight line has been related to the derivation, although it is a three-dimensional space straight line, but because it is a point-oriented relationship, the derivation process is still applicable to two-dimensional or even higher dimensions, so you can use the final conclusion of this article to fit a two-dimensional straight line, that is, the center of mass + the first eigenvector is the best fit straight line. 

#  Implementation code 

>  LineFit.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574092352
 ```  
#  III. Achieving results 

![avatar]( ee31711ca0d24152967e8b5bbb5d6769.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  I. Introduction 

>  In 1988, S. P. Tarasov, L. G. Khachiyan and I. I. Örlikh proposed the endoellipsoid method. For a detailed introduction to this method, please refer to this article: [Academic] Black Box Convex Optimization, Center Method and Khachiyan Constant Conjecture, and the relevant derivation process can also be found in this article: https://zhuanlan.zhihu.com/p/427628844. 

#  Code implementation 

>  main.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574032273
 ```  
>  DrawEllipseV1.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574032273
 ```  
>  MinVolEllipseV1.m 

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574032273
 ```  
#  III. Achieving results 

![avatar]( 415b24e0be2a4da4bae796fb407acc12.png) 

![avatar]( f06448f312b3490c886728df568ad98b.png) 



--------------------------------------------------------------------------------

#  Point cloud clustering 

#  Point cloud filtering 

#  Point cloud registration 

#  Point cloud segmentation 

#  Point Cloud IO 

#  Point cloud geometric shape 

#  Point cloud feature descriptor 

#  Forestry applications 

#  Depth image 

#  Point cloud sampling 

#  Kdtree and octree 

#  Point cloud rotation 

#  Point cloud characteristics 

#  other 



--------------------------------------------------------------------------------

