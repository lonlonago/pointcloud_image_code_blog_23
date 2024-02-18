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

