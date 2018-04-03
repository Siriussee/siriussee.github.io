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
        - [一个太阳系](#一个太阳系)
            - [公转逻辑](#公转逻辑)
            - [自转逻辑](#自转逻辑)
        - [牧师与恶魔](#牧师与恶魔)

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

利用 [transform.Translate](https://docs.unity3d.com/ScriptReference/Transform.Translate.html) 函数，实现向某方向移动物体多少距离的功能。

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

> 其实就是无限延申

```c#
public class parabola3 : MonoBehaviour {
    public float acceleration = 1;
    public float speed = 1;
    void Update () {
     transform.position = Vector3.MoveTowards(this.transform.position,
         this.transform.position + new Vector3(-1, 
         Time.deltaTime - 2 * this.transform.position.x) * Time.deltaTime,
         speed*Time.deltaTime);
    }
}
```

### 一个太阳系

先按照直觉，利用 GameObject 的 Sphere 搓出几个大小不一的球，然后按照太阳系的关系组织大小/距离和文件结构。

得到一个排列整齐的太阳系。下面进行公转和自转的逻辑的编写。

#### 公转逻辑

一开始设定的是公转速度是随机数，运行后发现明显违反了直觉的物理规律。

参考别人的博客之后，利用了物理学公式来使速度变得更合理。

利用随机数创造一个向量，使行星的旋转不共面。

```c#
public class rotation : MonoBehaviour {
    public Transform father;
    private float r;
    private float r_x;
    private float r_y;
    // Use this for initialization
    void Start()
    {
        r = this.transform.position.x;
        r_x = Random.Range(1, 3);
        r_y = Random.Range(1, 3);
    }

    // Update is called once per frame
    void Update()
    {
        Vector3 axis = new Vector3(r_x, r_y, 0);
        float speed = 200.0f * Mathf.Sqrt(1.0f / (r * r * r));
        this.transform.RotateAround(father.position, axis, speed * Time.deltaTime);
    }
}
```

#### 自转逻辑

```c#
    void Update()
    {
        this.transform.RotateAround(this.transform.position, Vector3.up, speed);
    }
```

### 牧师与恶魔

一个简单的游戏，就和狼和羊过河那个一样。

