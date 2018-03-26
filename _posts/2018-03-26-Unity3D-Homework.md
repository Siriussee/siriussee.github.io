---
layout:     post
title:      "Unity3D 基本概念与井字棋"
subtitle:   "第一次作业提交"
date:       2018-03-26 23:00:00
author:     "Sirius"
header-img: "img/u3d-bg-img.png"
tags:
    - Unity3D
    - homework
---

> 写在前面：
> 这是中山大学课程 [3D游戏编程与设计] 的课程博客。写就这篇博客的时候，我参考了为数众多的前人的文章；当然，我也同样欢迎您来参考和借鉴。不过，如果您执意要从我的文章中未经任何修改地复制大段文字和图片，**请仔细考量被判为抄袭的风险**。谢谢。

# 基本概念与我的第一个游戏

<!-- TOC -->

- [基本概念与我的第一个游戏](#基本概念与我的第一个游戏)
    - [基本概念](#基本概念)
        - [游戏对象和资源](#游戏对象和资源)
        - [MonoBehaviour 基本行为和常用事件](#monobehaviour-基本行为和常用事件)
        - [GameObject, Transform 与 Component](#gameobject-transform-与-component)
        - [描述 table 的对象属性，变换组件和组件](#描述-table-的对象属性变换组件和组件)
        - [对象的基本操作](#对象的基本操作)
        - [资源预设与对象克隆](#资源预设与对象克隆)
        - [组合模式](#组合模式)
    - [REFERENCE](#reference)

<!-- /TOC -->

## 基本概念

### 游戏对象和资源

- 出现在场景中的所有物体都是游戏对象(GameObject)，游戏对象按照一定的层次结构组织起来，显示在Hierarchy窗口中。对象（Object）是Unity创建的实例。资源通过文件夹的形式来组织，资源会按照文件类型分类放到不同的文件夹。
- 资源(Assets)就是可以在我们的项目中使用的文件，包括图像、视频、脚本文件、预制文件等，它们的存在不依赖于Unity。对象通过层次结构来组织，通过整体-部分的关系构成层次结构。
- 对象可以通过资源来保存起来，资源可以用来创建对象实例，一个资源可以创建多个对象。

###  MonoBehaviour 基本行为和常用事件

MonoBehaviour是每一个脚本对象的基类，这些方法会在运行的特定时间被调用

- 基本行为包括 `Awake()` `Start()` `Update()` `FixedUpdate()` `LateUpdate()`
- 常用事件包括 `OnGUI()` `OnDisable()` `OnEnable()`

创建 cube 对象，增加 script 组件，在 Assets 中添加 `NewBehaviourScript.cs` 文件，更改如下：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class NewBehaviourScript : MonoBehaviour {
	void Awake()
	{
		Debug.Log("IsAwake");
		this.enabled = true;
	}
	void FixedUpdate()
	{
		Debug.Log("IsFixedUpdate");
	}
	void LateUpdate()
	{
		Debug.Log("IsLateUpdate");
	}
	void Start () {
		Debug.Log("Start");
	}
	void Update () {
		Debug.Log("Update");
	}
	void OnGUI()
	{
		Debug.Log("OnGUI");
	}
	void OnDisable()
	{
		Debug.Log("OnDisable");
	}
	void OnEnable()
	{
		Debug.Log("OnEnable");
		this.enabled = true;
	}
}
```

点击上方 Play 按钮开始运行，得到输出如下：
![console-output](test-event-in-console)

可以得出结论，MonoBehaviour 事件的出发顺序是[1]：
![order](http://gad.qq.com/article/detail/28796)

### GameObject, Transform 与 Component 

查找[官方文档](https://docs.unity3d.com/Manual/class-GameObject.html)，文档对于这三个对象的解释如下：

- GameObjects are the fundamental objects in Unity that represent characters, props and scenery. 
- 游戏对象是在 Unity 中代表任务，道具和~~风景~~场景的基础对象。
- The Transform component determines the Position, Rotation, and Scale of each object in the scene. 
- 变换组件确定场景中每个对象的位置，旋转和缩放比例。
- Components are the nuts & bolts of objects and behaviors in a game. 
- 组件是游戏中对象和行为的细节。

### 描述 table 的对象属性，变换组件和组件

![sample-img]()

```json
GameObjects =
"name" : "table"
"layer" : "Default"
"tag"  "Untagged"
Transform = 
"Position": (0, 0, 0)
"Rotation": (0, 0, 0)
"Scale" : (1, 1, 1)
Components =
"Transform" : true
"Mesh-filter" : true
"Mesh-Renderer" : true
"Box-Collider" : true
```

使用 [UMLet](http://www.umlet.com/changes.htm) 画出 UML 图

![UML-of-sample]()

### 对象的基本操作

查找官方文档[2]，寻找对象基本操作函数

```C#
//查找对象
Find(name);
FindWithTag(tag)	//按标签查找
FindGameObjectsWithTag(tag)	//返回对象数组
//创建新的对象
CreatePrimitive(type);
Instantiate(source);	//通过复制创建对象
//遍历
foreach (Transform child in transform) {
    visit(child);
}
//销毁
foreach (Transform child in transform) {
    GameObject.Destroy(child);
}
```

### 资源预设与对象克隆

- 预设(prefab)是一个对象的快照或模板，可以用于快速生成相同的对象。修改预设以后，通过该预设生成的对象也会发生变化。
- 对象克隆(clone)复制一个原有的对象。但是克隆出的对象与源对象不再有联系。

使用预设生成一个 Table ：
```c#
GameObject TableClone = (GameObject)Instantiate(Resource.Load(TablePath);
```

### 组合模式

组合模式(Composite Pattern)允许你将对象组合成树形结构来表现“部分-整体”的层次结构，使得对象使用者以一致的方式处理单个对象以及对象的组合。

使用 BroadcastMessage() 方法向子对象发送消息：

```c#
public class ComputerScript : MonoBehaviour {//parent
   void Start () {
       this.BroadcastMessage("Boot"); //Broadcast Boot to child
   }
}

public class CPUscript : MonoBehaviour {//child
    void Boot() {//receive Boot message and exceute
        Debug.Log("Child Received");
    }
}
```

## REFERENCE

[1] [腾讯GAD游戏开发者社区](http://gad.qq.com/article/detail/28796)
[2] [官方文档](https://docs.unity3d.com/ScriptReference/Object.html)