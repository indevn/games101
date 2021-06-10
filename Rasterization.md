# Rasterization (lec 5,6)

**What is a screen?**

- an array of pixel(‘FYI’)

- Size of the array: resolution

- A typical kind of raster display

  (raster means screen in German. raserize means ‘drawing onto the screen’)

**What is pixel?**

- Color is a mixture of (red, green, blue)
- Pixels’ indices are from  (0, 0) to (width - 1, height - 1)
- Pixel (x, y) is centered at (x + 0.5, y + 0.5)
- The screen covers range  (0, 0) to (width, height)

**Canonical Cube to Screen**

1. Irrelevant to z

2. Transform in xy plane: $[-1, 1]^2$ to [0, width] x [0, height]

   Viewport transform matrix:

$$
M_{view}=
\begin{bmatrix}
\frac {width}{2}&0&0&\frac {width}{2}\\
0&\frac {height}{2}&0&\frac {height}{2}\\
0&0&1&0\\
0&0&0&1
\end{bmatrix}
$$

## Triangles: Fundamental Shape Primitives

**Why triangles?**

- Most basic polygon
  - Break up other polygons
  - Unique property
- Unique properties
  - Graranteed to be planar
  - Well-defined interior

**What Pixel Values Approximate a Triangle?**

- A Simple Approach: **Sampling**

  We can <u>discretize</u> a function by sampling. Sample if Each Pixel is inside triangle.

  1. Define binary function: inside(t,x,y)

     return 1 if Point (x,y) in triangle t, or return 0

     **Realization:** The Cross Products 

     

     $\vec {P_1P_2} \times \vec {P_1Q} > 0$ if Q is locating left side of $\vec {P_1P_2}$<img src="Rasterization.assets/image-20210610212144915.png" alt="image-20210610212144915" style="zoom:33%;" />

     We could realize inside() after 3 times judgement.

     *Edge Cases: it depends*

  2. Sampling a 2D indicator function

     ```cpp
     for (int x = 0; x < xmax; ++x) 
     	for (int y = 0; y < ymax; ++y) 
     		image[x][y] = inside(tri,x + 0.5,y + 0.5);
     ```

     **Optimize**: no need to checking all pixels on the screen

     - check each vertex before use a Bouding Box(AABB).

     - Suitable for thin and rotated triangles.

       

### Fishing up

