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

