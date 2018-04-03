---
layout:     post
title:      "Unity3D 空间运动与牧师过河"
subtitle:   "第二次作业提交"
date:       2018-04-03 23:00:00
author:     "Sirius"
header-img: "img/u3d-bg-img.png"
tags:
    - Unity3D
    - homework
---

> 写在前面：
> 这是中山大学课程 [3D游戏编程与设计] 的课程博客。写就这篇博客的时候，我参考了为数众多的前人的文章；当然，我也同样欢迎您来参考和借鉴。不过，如果您执意要从我的文章中未经任何修改地复制大段文字和图片，**请仔细考量被判为抄袭的风险**。谢谢。

# 空间运动与牧师过河

<!-- TOC -->

- [空间运动与牧师过河](#空间运动与牧师过河)
    - [Unity3D 的空间运动](#unity3d-的空间运动)
        - [游戏对象运动的本质是……](#游戏对象运动的本质是)
        - [茴字的三种写法](#茴字的三种写法)
            - [直接修改 transform 属性](#直接修改-transform-属性)
            - [transform.Translate](#transformtranslate)
            - [Vector3.MoveTowards](#vector3movetowards)

<!-- /TOC -->

## Unity3D 的空间运动

### 游戏对象运动的本质是……

Transform组件的属性值的变换！也就是坐标的变化！

### 茴字的三种写法

#### 直接修改 transform 属性

acceleration 代表加速度。虽然在这个代码中使用加速度这个概念不是很准确，但是在物理运动里面这样表述还是相对科学的。

```C#
public class parabola1 : MonoBehaviour
{
    public float acceleration = 1;
    public float speed = 10;
    void Update()
    {
        this.transform.position += Vector3.down * Time.deltaTime * speed * acceleration;//s = (at^2)/2 = avt/2
        this.transform.position += Vector3.right * Time.deltaTime * speed;//s = vt
        acceleration++;
    }
}
```

#### transform.Translate

利用 [transform.Translate](https://docs.unity3d.com/ScriptReference/Transform.Translate.html) 函数，实现 向某方向移动物体多少距离 的功能。

使用一个与时间有关的三维向量作为移动的速度。在本例中 x轴匀速运动， y轴加速运动，z轴静止。

```c#
public class parabola2 : MonoBehaviour {
    public float acceleration = 1;
    public float speed = 10;
    void Update ()
    {
        transform.Translate(new Vector3(Time.deltaTime * speed, Time.deltaTime * acceleration, 0));
        acceleration++;
    }
}
```

#### Vector3.MoveTowards

同理，使用一个与时间有关的三位速度向量。

从 当前位置 transform.position，移向目标位置 new Vector3，最大长度随时间延长

> 其实就是无线延申

```c#
public class parabola3 : MonoBehaviour {
    public float acceleration = 1;
    public float speed = 10;
    void Update()
    {
        float step = speed * Time.deltaTime;
        transform.position = Vector3.MoveTowards(transform.position, new Vector3(Time.deltaTime * speed, Time.deltaTime * acceleration, 0), step);
        acceleration++;
    }
}
```