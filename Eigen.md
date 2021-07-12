# Eigen

## Matrix模板类

```
class Eigen::Matrix< _Scalar, _Rows, _Cols, _Options, _MaxRows, _MaxCols >
```

参数：

`_Scalar` 元素标量类型

`_Rows` `_Cols` 编译时行和列的值



特殊的矩阵：

```cpp
typedef Matrix<float, 3, 1> Vector3f;
typedef Matrix<int, 1, 2> RowVector2i;
typedef Matrix<double, Dynamic, Dynamic> MatrixXd; // 动态大小的矩阵
typedef Matrix<int, Dynamic, 1> VectorXi; // 动态大小的向量
```

### 构造与初始化

```cpp
//构造器
Matrix3f a;
MatrixXf a(10,15);
Matrix3f a(3,3); // 在固定类型矩阵上指定大小是合法的

// 对短的向量元素提供初始化方法
Vector2d a(5.0, 5.0);

// 输入流，逗号分隔
Eigen::Matrix3f m;
m << 1, 2, 3,
     4, 5, 6,
     7, 8, 9;
  std::cout << m;

// Constructors：
Vector4d  v4;
Vector2f  v1(x, y);
Array3i   v2(x, y, z);
Vector4d  v3(x, y, z, w);
 
VectorXf  v5; // empty object
ArrayXf   v6(size);
Matrix4f  m1;
 
MatrixXf  m5; // empty object
MatrixXf  m6(nb_rows, nb_columns);

// Comma initializer
Vector3f  v1;     v1 << x, y, z;
ArrayXf   v2(4);  v2 << 1, 2, 3, 4;
Matrix3f  m1;   m1 << 1, 2, 3,
                      4, 5, 6,
                      7, 8, 9;
                      
// Comma initializer (bis)	
int rows=5, cols=5;
MatrixXf m(rows,cols);
m << (Matrix3f() << 1, 2, 3, 4, 5, 6, 7, 8, 9).finished(),
     MatrixXf::Zero(3,cols-3),
     MatrixXf::Zero(rows-3,3),
     MatrixXf::Identity(rows-3,cols-3);
cout << m;  
```




## 矩阵分块

```
x.head(n)		// (1:n) 提取前n个vector，index从0到n-1
```

