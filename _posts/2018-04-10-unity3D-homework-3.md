---
layout:     post
title:      "镜头、背景与动作分离"
subtitle:   "第三次作业提交"
date:       2018-04-10 23:00:00
author:     "Sirius"
header-img: "img/u3d-bg-img.png"
tags:
    - Unity3D
    - homework
---

# 镜头、背景与动作分离

<!-- TOC -->

- [镜头、背景与动作分离](#镜头背景与动作分离)
    - [镜头的设置](#镜头的设置)
    - [背景的设置](#背景的设置)
        - [天空盒 skybox](#天空盒-skybox)
        - [地形 Terrian 和水](#地形-terrian-和水)
    - [动作分离](#动作分离)
    - [遇到的一些问题](#遇到的一些问题)

<!-- /TOC -->

这个是[我的项目文件](https://github.com/Siriussee/Unity3D-hw/tree/master/my_devil)

## 镜头的设置

镜头分为透视和正交两个模式。利用垂直向下的正交镜头可以实现小地图的功能。

> 可惜我没空做。

我利用了主镜头和一个分镜头，增加了一个可以切换视角的功能。

![top view](http://ovi1rdu1p.bkt.clouddn.com/hw3-top.png)
![front view](http://ovi1rdu1p.bkt.clouddn.com/hw3-front.png)

当然啦，因为主镜头没有办法动态生成（也或者是我找不到动态生成的方法），所以只能用 `find()` 方法来取到 Camera 。

在这一块稍微违反了 MVC 模式的要求；不过，效果还是很好的实现了的。

实现的代码如下：

```c#
//去掉了无关部分的代码
public class UserGUI : MonoBehaviour
{
    private GameObject Camera1;
    private GameObject Camera0;
    void Start()
    {
        Camera0=GameObject.Find("Main Camera");
        Camera1=GameObject.Find("Camera1");
        Camera1.active = true;
        Camera0.active = false;
    }
    void OnGUI()
    {
        if(GUILayout.Button("Front",buttonStyle)){
            Camera0.active=true;
            Camera1.active=false;
        }

        if(GUILayout.Button("Top",buttonStyle)){
            Camera0.active=false;
            Camera1.active=true;
        }
    }
}

```

## 背景的设置

这一部分主要分为天空盒 skybox，地形 Terrian 和水的部分。

![mt and water](http://ovi1rdu1p.bkt.clouddn.com/hw3-mount%20and%20water.png)

### 天空盒 skybox

天空盒的制作主要参考了潘老师的PPT。

首先下载 Skyboxes.zip 解压后直接把想用的那个天空盒的文件夹拖入 Asset 中。

创建 shader，将属性选为 skybox ，将文件夹中的对应图片拖入框中，即可自动生成完整的天空盒。

给相机添加天空盒的组件，然后把生成的天空盒拖入，成功！

### 地形 Terrian 和水

在 GameObject 中创建地形，使用笔刷刷出心目中的地形。

在 Asset 中导入材质包，选取一个合适的山地材质包导入。此外，顺便也把 Ocean 和你喜欢的水材质包也导入。

放置山地材质；放置 Ocean 并且放上水材质包。

完成。最终实现效果如下。

<video src="http://ovi1rdu1p.bkt.clouddn.com/hw3-unity-compressed.mp4" width="720" height="540" controls="controls">
Your browser does not support the video tag.
</video>

> 啊，这光；啊，这水。

## 动作分离

这一部分参考了老师的课件示例代码，也有赖于 Nash 同学一个下午的 P2P debug。

首先是PPT中展示的类的关系：

![UML](http://ovi1rdu1p.bkt.clouddn.com/hw3-action-UML.png)

> 此图片版权归 C486C@CSDN https://blog.csdn.net/c486c/article/details/79854679 所有。

接下来，逐个阐述各个组件的功能和含义

```c#
public enum SSActionEventType:int {Started,Completed}
```
动作事件状态类型。枚举类，描述事件的状态——开始、完成

```C#
public interface ISSActionCallback{
    void SSActionEvent(SSAction source,
        SSActionEventType events = SSActionEventType.Completed,
        int intParam = 0,
        string strParam = null,
        Object ObjectParam = null);
}
```
事件完成回调函数接口。声明了回调函数的接口，所有有动作需要回调的类都必须继承并且实现它。

> 虽然到头来并没有需要用回调来实现的动作/效果。因此也就不需要在实现中邪什么代码了。

```c#
public class SSAction : ScriptableObject {
    public bool enable = true;
    public bool destory = false;
    public GameObject gameobject { get; set;}
    public Transform transform { get; set;}
    public ISSActionCallback callback { get; set;}
    protected SSAction();
    public virtual void Start () ;
    public virtual void Update ();
}
```
动作。抽象类/基类，不允许显式和隐式创建实例，有待下文实现其中的方法。继承 ScriptableObject 代表不受 Gameobj 绑定限制。

```c#
public class CCMoveToAction : SSAction{
    public Vector3 target;
    public float speed = 10;
    public static CCMoveToAction GetAction(Vector3 target, float speed);
    public override void Start ();
    public override void Update();
}
```
【移动到】动作。动作类的实现，用于物体的位移。

```c#
public class CCSequenceAction : SSAction, ISSActionCallback{
    public List<SSAction> sequence;
    public int repeat = -1;
    public int start = 0;
    public void SSActionEvent(SSAction source,    SSActionEventType events,int intParam,string strParam ,Object ObjectParam);//实现ISSActionCallback
    public static CCSequenceAction GetSSAction(int repeat, int start, List<SSAction> sequence);
    public override void Update();
    public void SSActionEvent (SSAction source, SSActionEventType events = SSActionEventType.Completed);
    public override void Start();
    void OnDestory();//释放内存
}
```
【移动到】动作序列。或者可以理解为组合动作，可以保存一组动作，然后依次执行并在结束时调用回调函数，最后释放自己。

```c#
public class SSActionManager :MonoBehaviour, ISSActionCallback{
    private Dictionary<int, SSAction> actions = new Dictionary<int,SSAction>();
    private List<SSAction> waitingAdd = new List<SSAction>();
    private List<int> waitingDelete = new List<int>();
    public void SSActionEvent(SSAction source,    SSActionEventType events,int intParam,string strParam ,Object ObjectParam);
    protected void Update();
    public void RunAction(GameObject gameobject, SSAction action ,ISSActionCallback manager);
    protected void Start();
}
```
动作管理类。管理上面的【移动到】动作和【移动到】动作序列，建立了一个字典来存放全部的动作，然后在 `update()` 函数中一个个把他们完成掉。虽然说在这么一个结构比较简单的游戏里面比较多余，但是既然放进PPT了那就干脆也对着敲下来算了……

```c#
public class MySSActionManager : SSActionManager{


        public void MoveBoat(BoatController BoatController){
            CCMoveToAction action = CCMoveToAction.GetAction (BoatController.getEmptyPosition(), 20f);
            RunAction (BoatController.getGameobj(), action, this);        
        }    

        public void MoveCharacter(MyCharacterController characterCtrl, Vector3 destination) {
            
            Vector3 currPos = characterCtrl.getCharacter().transform.position;
            Vector3 midPos = currPos;

            if (destination.y > currPos.y) 
                midPos.y = destination.y;
            else 
                midPos.x = destination.x;
            
            SSAction action1 = CCMoveToAction.GetAction(midPos, 20f);
            SSAction action2 = CCMoveToAction.GetAction(destination, 20f);
            SSAction seqAction = CCSequenceAction.GetSSAction(1, 0, new List<SSAction> { action1, action2 });

            RunAction(characterCtrl.getCharacter(), seqAction, this);
        }    
}
```
动作管理类的实现。把动作管理与游戏的实际动作链接起来，负责【将什么样的动作放入序列】，并交付动作管理类执行。

除此之外只需要把之前上一个版本的动作函数替换成动作管理类的实现中的 `MoveBoat(BoatController BoatController)` `void MoveCharacter(MyCharacterController characterCtrl, Vector3 destination)` 就大功告成了！

## 遇到的一些问题

这个类太多就很容易遇到逻辑上构成混乱的问题，也正是看了 Nash 同学画的 UML 图我才搞懂它们之间有什么关系。

我栽倒过的几个类如下：

```c#
public class MyFirstController : MonoBehaviour,SceneController ,UserAction{
    public MySSActionManager MySSActionManager;
}
```
我一开始以为这个控制器会控制全部动作，所以要继承一下 MySSActionManager ，结果疯狂报错，debug 半小时。结果最后是用过带一个 MySSActionManager 的引用来实现的。


```c#
public class SSActionManager :MonoBehaviour,ISSActionCallback{
    public void SSActionEvent(SSAction source,SSActionEventType events,int intParam,string strParam ,Object ObjectParam){}
```
我一开始看着上面 CCSequenceAction 已经实现了回调函数的接口了，就没有必要再在管理类里面再继承并且实现一次了，结果又报错 `no impl` ，又重新看了一眼，将信将疑的把实现加上去。

--EOF--