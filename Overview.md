# Overview

## L1-Overview

- Course Topics 大致分为四个Part：光栅化、几何、光线追踪、动画和模拟

- 一些补充：

- - 光栅化：三维空间的几何形体显示在屏幕上
  - 图形学中的“实时”：30fps →其他的：offline（离线）

## L2-线代复习

- 向量

- - 概念
  - 运算
  - 点积的应用（找夹角、投影、判断前后/接近程度）
  - 叉积的应用（右手坐标系、判断左右/内外）

- 右手坐标系

- 矩阵

- - 概念（能乘的情况、如何乘（一个很好的记忆方法）、转置、逆、）
  - 矩阵和向量的乘法
  - 向量和向量的点积、叉积都能写成矩阵和向量的乘的形式

## L3-变换1（2D）

- 2D Transformation

- - 线性变换=矩阵
  - 线性变换（缩放、反射、切变、旋转）

- 齐次坐标

- - 引入：平移不属于线性变换，为了统一
  - 齐次坐标的具体内容
  - 仿射变换=线性+平移
  - 齐次坐标下的2DTransforms
  - 逆变换：就是乘以变换矩阵的逆矩阵

- 组合变换

- - 复杂的变换都是由基础的变换组合而来
  - 注意矩阵的左乘、无交换律

- 3D Transformation

- - 齐次坐标下的三维向量和点

## L4-变换2（MVP）

- 对L3的补充

- - 推导：在旋转中，逆=转置 数学上：一个矩阵的逆=转置 →正交矩阵
  - 齐次坐标下的3D仿射变换矩阵
  - 复杂的旋转：欧拉角
  - 罗德里格斯旋转公式（任意轴的旋转表示）
  - △ 四元数，更多的为了旋转间的插值（没有讲，自行扩展）

- 观测变换（Viewing transformation）

- - 观测变换和视图变换的区别：观测变换包括视图变换和投影变换

  - MVP的理解

  - View矩阵的定义和推导

  - Projection矩阵的定义和推导

  - - 正交矩阵
    - 透视矩阵

## L5-光栅化1（三角形的离散化）

- 准备工作

- - 定义fov

- mvp之后得到cube[-1，1]3 ，要画在屏幕上

- - 定义屏幕空间

  - 一些解释

  - - Raster就是德语中的Screen
    - pixel

- 正式进入光栅化

- - 一些光栅显示设备

  - 如何画在屏幕上：光栅化

  - 为什么是三角形/三角形的性质

  - 光栅化的关键：如何判断一个像素和三角形的位置关系（像素中心点与三角形的位置关系）

  - 判断方法：采样。

  - - 采样的感性认知

    - 采样的具体实现：

    - - 判断像素中心是否在三角形内：定义一个inside函数
      - 叉积→全负/正即为三角形内

## L6-光栅化2（深度测试、抗锯齿）

- 采样理论

- - 采样的artifacts
  - 走样的原因
  - 反走样的一个想法：采样前做一个模糊

- 频域

- - 举例
  - 傅里叶变换
  - 从频率看 走样的定义

- Filtering 滤波

- - 定义

  - 傅里叶变换的作用：把一个函数从时域变换到频域

  - 不同滤波的效果

  - 滤波=卷积=平均

  - 卷积的定义

  - 卷积定理，做卷积的两种操作

  - - Operation1：图和滤波器直接在时域上做卷积操作
    - Operation2：先把图傅里叶变换，变换到频域上，把滤波器变到频域上，两者相乘；乘完之后再逆傅里叶变换到时域上

  - Box Filter-卷积盒（低通滤波器）：时域上变大 → 频域上变小

- 采样

- - 定义
  - 走样的原因

- 反走样

- - 操作1：提升出采样率（不是反走样）
  - 操作2：Antialiasing：先做一个模糊再采样

- 实际的反走样

- - MSAA
  - 提到的其他的：FXAA、TAA、超分辨率

## L7＆L8着色1、2（光照、着色模型、着色频率、图形管线、纹理映射）

- 画家算法作为引题-远近处的问题

- Z-buffer深度缓冲

- - 对深度(测试)的理解
  - 核心思想
  - 伪代码
  - 一个例子

- Shading（local概念）

- - 图形学上的应用

  - Blinn-Phong着色模型

  - - 漫反射项

    - - Lambert余弦定理
      - 具体内容

    - 高光项

    - - 具体内容

    - 对于公式的一些补充（为什么ks是白色、p次方的作用等）

    - 环境光项：是假设的

    - 总结

- 着色频率

- - 感性认识（配图）

  - 正规定义

  - - Flat Shading 逐表面
    - Gouraud Shading 逐顶点
    - Phong Shading 逐像素
    - 定义逐顶点
    - 定义逐像素

- 渲染管线

- - 总览
  - 用mvp来举例
  - shader概念的完善
  - GPU

- 纹理映射

- - 对物体表面的理解

  - 举例讲解

  - - 物体映射到纹理
    - 纹理的坐标系：uv
    - 纹理的无缝衔接

  - 纹理和着色的区别和联系

## L9-着色3（插值、高级纹理映射）

- 重心坐标

- - 做插值的"三问"（what why how）
  - 重心坐标的定义
  - 三角形顶点的中心坐标
  - 另一种定义：重心坐标可以通过面积算
  - 重心的坐标表示
  - 任意一点的坐标表示
  - 注意点：重心坐标不能保证投影后不变 →先找到重心做插值再投影

- 应用纹理

- - Diffuse Color：用贴图映射漫反射颜色

  - Texture Magnification纹理放大

  - - 纹素（texel）的解释

    - 纹理太小的情况

    - - 双线性插值
      - 双向三次插值

    - 纹理太大的情况（按上边操作会产生摩尔纹）

    - - 原因：像素覆盖的纹理区大的时候，不能用pixel中心简单采样

      - 解决方法

      - - 超采样-MSAA（代价大）
        - Mipmap：每一层分辨率变为原来的一半**。**
        - 具体做法
        - 三线性插值（查找连续的层）
        - 局限性：Overblur过度模糊
        - 过度模糊的解决：
        - 各向异性过滤
        - EWA过滤

## L10-几何1（简介）

- 补充L9：纹理的其他应用

- - 环境贴图/光照

  - - 环境贴图
    - 环境光记录在秋上
    - Cubemap

  - 纹理可以影响shading

  - - Bump mapping凹凸贴图
    - Displacement mapping位移贴图

  - 三维纹理：定义噪声函数来变成我们想要的样子

  - Texture可以记录一些已经算好的信息

  - 3D Texture 和体积渲染

- 几何部分

- - 几何的例子

  - 几何的简单分类

  - - 隐式几何
    - 显式几何

  - 几何的更多表示方法

  - - 隐式（数学公式、基本几何运算定义复杂几何、距离函数、Blending Distance Functions、Level Set Methods 水平集、Fractals 分形（自相似））

    - 显式（点云、多边形面/三角形面）

    - - .obj

## L11-几何2（曲线和曲面）

- 曲线

- - 贝塞尔曲线

  - de Casteljau Algorithm（算法）：如何用任意多个点画出一条贝塞尔曲线

  - - 三个点情况
    - 四个点情况

  - 贝塞尔曲线的代数表示

  - 贝塞尔曲线的性质

  - Piecewise（逐段） 贝塞尔曲线

  - 其他种类的splines（样条）

  - - Splie的定义
    - B-spline（basis（基函数） spline）---对贝塞尔去曲线的扩展

- 曲面

- - 贝塞尔曲面

## L12-几何3（曲面和光栅化部分的补充：阴影）

- 曲面

- - 网格细分

  - - Loop Subdivision为例
    - Catmull-Clark Subdivision (General Mesh) 为例

  - 网格简化

  - - 在不同情况应该用不同复杂度的模型
    - 怎么计算：
    - edge collapsing 边塌缩（核心算法、实际操作）

- 光栅化部分的补充：shadow-阴影

- Shadow mapping

- - 概述
  - Key Idea（两个pass的做法）
  - 一个实例:用Shadow mapping的方法生成 shadow map 并应用它生成shadow

- 阴影的问题

- - 硬阴影
  - 软阴影（GAMES202中有讲）

## L13-光线追踪1（Whitted-Style Ray Tracing）

- 为什么引入光追（光栅化的缺点、和光追的区别）

- Basic Ray-Tracing Algorithm

- - 定义光线
  - 光线投射-Ray Casting

- Recursive (Whitted-Style) Ray Tracing

- 技术问题：求交点

- - 定义射线

  - 求光和球的交点

  - 和隐式表面的交点

  - 和显式表面的交点

  - - why

    - 怎么计算

    - - 每个三角形都算（很慢）
      - Möller Trumbore Algorithm（MT算法）：想直接求出光和三角形的交点，立即判断是否在三角形内

  - 光线和表面求交的加速

  - - 一个重要概念Bounding Volumes（包围盒/体积）

    - 长方体

    - 通常用的：Axis-Aligned Bounding Box (AABB) 轴对齐包围盒

    - - 2D情况

      - 3D情况

      - - key idea
        - 算法

    - 总结

## L14-光线追踪2（加速结构）

- 均匀格子

- - 预处理
  - 衡量效果：网格分辨率
  - 均匀格子能处理好/不能处理好的情况

- 空间划分

- - Oct-tree 八叉树（三维均匀切分）（与维数有关）

  - KD-Tree （几乎和八叉树相同）每次只沿某一个轴划分

  - BSP-Tree 每次取一个方向（非横平竖直）将空间分为两部分 （会很麻烦）

  - KD树的详细内容

  - - 例子
    - 数据结构
    - 实际如何用- - - 难题（物体划分来解决）

- 物体划分

- - BVH

  - - 操作
    - 能避免kd树的两个问题
    - 自身引起的问题

  - 如何划分

  - BVH的数据结构

  - 算法

- 空间划分和物体划分的区别

- 辐射度量学

- - 老三问

  - why（辐射度量学：精准度量光的一系列物理量→以物理上正确的方式来计算光照

  - what 定义了光照的一些属性 ：Radiant flux, intensity, irradiance, radiance

  - how

  - - 通过两个定义来研究其他物理量：Radiant Energy ＆ Flux (Power)

    - Radiant Intensity

    - - 定义
      - 立体角-solid angle

## L15-光线追踪3（辐射度量学、渲染方程、全局光照）

- 辐射度量学继续讲

- - Irradiance
  - Radiance
  - 比较Intensity、Irradiance、Radiance
  - Incident Radiance、Exiting Radiance
  - 区别Irradiance和Radiance

- 光线传播（反射方程、渲染方程、全局光）

- BRDF（双向反射分布函数）Bidirectional Reflectance Distribution Function

- - 试图用 “Radiance →积分得→ Irradiance”来解释BRDF
  - BRDF的定义（其实就是一个比例：对于任何一个出射方向，算出来他的Radiance，除以dA接受到的Irradiance，就是BRDF）

- 反射方程

- 渲染方程（ 是通用化的过程，渲染方程 = 自己产生/发射出的 + 反射方程）

- - 通用化
  - 理解渲染方程是怎么来的
  - 问题理解为递归

- 全局光照的概念（全局光照=直接光照+间接光照）

- 概率论复习

- - 随机变量、变量
  - 概率
  - 期望
  - pdf（概率密度函数）：连续情况下描述变量如何分布
  - 随机变量函数

- 这节课总结

## L16-光线追踪4（蒙特卡洛积分、路径追踪）

- Monte Carlo Integration蒙特卡洛积分

- - why：为了解决定积分
  - 定义
  - 用蒙特卡洛方法计算

- 路径追踪

- - 回顾Whitted风格的光追的问题

  - 路径追踪- - -改良Whitted风格的光追非基于物理的问题

  - 两个难题：

  - - ①半球积分：蒙特卡洛方法解决
    - ②递归问题：解决停不下来：俄罗斯轮盘赌

  - 具体解决过程

  - 已经正确 → 不浪费的算法

- 现在和过去的光追的概念

- 本课程没有谈的话题

## L17-材质和外观

- 渲染方程中，BRDF项和材质有关 → Material= =BRDF

- 漫反射

- Gloosy material（BRDF）

- Ideal reflective / refractive material (BSDF*)

- BSDF=BRDF+BTDF

- - 具体内容
  - 全反射现象：BTDF

- 菲涅尔项

- - 理解
  - 计算

- 微表面材质

- - 微表面理论
  - 微表面BRDF

- 区分材质的一类方法

- - 材质分为两类：各向异性、各向同性
  - 具体内容
  - 各向异性BRDF

- BRDF的属性/性质（非负、线性、可逆、能量守恒、各向异性/各向同性）

- 测量BRDF

- - why
  - how
  - then？
  - 一个有名的BRDF库：MERL BRDF Database

## L18-高级光线传播与外观建模

- 高级光线传播

- - 有偏和无偏的解释
  - 双向路径追踪（BDPT）
  - Metropolis光线传播（MLT

- 有偏的

- - 光子映射（Photon Mapping）

  - - 擅长做什么
    - 具体做法
    - 细说

  - VCM (Vertex Connection and Merging)

  - - 结合了光子映射和双向路径追踪

  - Instant Radiosity实时辐射度算法

  - - 已经照亮的面都认为是光源，再照亮其他地方
    - →优缺点

- 高级外观建模

- - 非表面

  - - Participating media （如，云、雾）
    - Hair/fur/fiber（BCSDF）
    - Granular material（颗粒材质）

  - 表面

  - - Translucent material (BSSRDF)半透明材质

    - Cloth布料

    - Detailed material (non-statistical BRDF)复杂的材质

    - - 对微表面模型的BRDF进行完善
      - 不同法线贴图的效果

    - 程序化生成材质

    - - 定义
      - 和Houdini不同

## L19-**相机、透镜**

- 成像方法

- 相机

- - 小孔成像

  - FOV

  - - 定义
    - 焦距（Focal Length）
    - 传感器大小（Sensor Size）

  - Exposure 曝光

  - 影响成片亮度的因素

  - - 光圈
    - 快门速度
    - ISO gain（感光度）
    - 快门速度的应用：高速、延时摄影

- 透镜

- - Thin Lens Approximation薄透镜近似
  - 假设焦距可以任意改变
  - Defocus Blur （焦散模糊 - 可以解释景深）
  - 光圈的定义
  - 光追中理想薄透镜
  - Depth of Field景深

## L20-光场、颜色

- 光场

- - 我们看到的世界
  - 全光函数
  - 光场
  - 光场camera

- 颜色

- - 牛顿的实验

  - - 白光是所有颜色叠加起来的结果
    - 波长-折射率
    - 光对应光谱
    - 谱功率密度(SPD)

  - 颜色

  - - 是人的感知
    - 人眼结构
    - 是怎么感知的
    - Metamerism同色异谱
    - color matching

  - 颜色空间

  - - 标准RGB系统（sRGB）
    - CIE XYZ
    - 色域
    - 其他颜色空间（H-S-V、CIE LAB、CYMK）

- 本节课没提到的

- - HDR
  - 伽马校正

## L21-动画与模拟

- 历史

- Keyframe Animation关键帧动画

- - 本质
  - 做法

- Physical Simulation物理模拟

- - 牛顿定律

  - 质点弹簧系统

  - - 分析
    - 改进

- 粒子系统

- - - 概述
    - 简单的算法
    - 进一步认识

- Kinematics 运动学

- - 正向运动学
  - 逆运动学

- Rigging（绑定？）

- - 概念
  - Blend shapes

- 动捕

- 恐怖谷效应

- 生产管线

## L22-欧拉方法、刚体模拟、流体模拟

- 一个粒子的模拟

- 常微分方程

- - 定义
  - 解：欧拉方法
  - 欧拉方法的问题：不准、不稳定

- 解决不稳定

- - Midpoint Method中点法
  - Adaptive Step Size自适应步长
  - Implicit Euler Method 隐式/后向欧拉方法

- Position-Based / Verlet Integration不是基于物理的方法

- - 刚体模拟

  - 流体模拟

  - - 思路
    - 更新
    - 欧拉方法和拉格朗日方法（支点法和网格法）的区别

- 今后学习路径的建议
