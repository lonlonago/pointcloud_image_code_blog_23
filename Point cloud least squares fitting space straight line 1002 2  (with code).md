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

