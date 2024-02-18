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

