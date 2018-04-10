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
            - [游戏中的对象](#游戏中的对象)
            - [游戏的设计](#游戏的设计)
                - [MVC 的结构](#mvc-的结构)

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

![soalrsystem](http://ovi1rdu1p.bkt.clouddn.com/solaysys.png)

### 牧师与恶魔

一个简单的游戏，就和狼和羊过河那个一样。

#### 游戏中的对象

- 三个恶魔和三个牧师：在船-岸之间往复移动。
- 一艘船：带有两个空槽，可以在两岸往复运动。存在游戏胜利的判定。
- 两岸：各自带有六个空槽。存在游戏胜利的判定。
- 水：只是背景。

#### 游戏的设计

由于要由空对象生成全部的对象，而且要使用MVC的结构程序，我智商捉急，就去参考了一下[优秀程序](https://www.jianshu.com/p/07028b3da573)，在理解的基础上完成了自己的游戏。

##### MVC 的结构

这个 Unity 的 MVC 结构要比我一开始想的类 Java 的 MVC 结构更加复杂一点，整体的逻辑构成如下：

```
Director
|-  (SceneController)FirstController ~ (UserAction)ClickGUI
    |-  (Moveable)MyCharacterController 
    |-  (Moveable)BoatController
    |-  CoastController
```

简言之，与我以前接触的 MVC 模式相比，就是增加了

- 导演。这一部分相当于给程序多包了一层，问题不大。
- 门面模式。这个东西是C-V之间的一个接口，相当于是给点击这个动作做了一个封装，封装为了一个函数，进一步降低了模块之间的耦合程度。

这个是[我的项目文件](https://github.com/Siriussee/Unity3D-hw/tree/master/my_devil)

<video src="http://ovi1rdu1p.bkt.clouddn.com/unity-hw2.mp4" width="720" height="540" controls="controls">
Your browser does not support the video tag.
</video>